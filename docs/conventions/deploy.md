# Puesta en marcha del entorno CI/CD

> Cómo se levanta, verifica y detiene la infraestructura de CI/CD de AuthApp CI.
> Este es un proyecto educativo: **no hay despliegue de la aplicación a
> ambientes** (dev/staging/prod). Lo que se opera es el entorno local de
> integración continua (Jenkins + SonarQube) mediante Docker Compose.
> **Última actualización**: 2026-07-02

## Stack de infraestructura

- **Contenedores / orquestación**: Docker + Docker Compose.
- **Servidor de CI**: Jenkins (construido desde `Dockerfile`, expone el puerto 8080).
- **Análisis de calidad**: SonarQube (`sonarqube:lts`, expone el puerto 9000).

## Entorno

Solo existe un entorno: **local**, levantado en la máquina del desarrollador.

| Servicio  | URL                     | Puerto |
| --------- | ----------------------- | ------ |
| Jenkins   | http://localhost:8080   | 8080   |
| SonarQube | http://localhost:9000   | 9000   |

## Reglas

- Cada arranque debe ser reproducible: toda la configuración vive en `docker-compose.yml` y el `Dockerfile`.
- Los secretos (p. ej. el token de SonarQube) se gestionan según [`secrets.md`](secrets.md); nunca se commitean.
- Verificar que ambos servicios respondan tras levantar el entorno.

## Puesta en marcha

```bash
# Levantar Jenkins y SonarQube (construyendo las imágenes) en segundo plano
docker compose up --build -d
```

## Verificación (health checks)

- Jenkins responde en http://localhost:8080
- SonarQube responde en http://localhost:9000

```bash
curl -I http://localhost:8080   # Jenkins
curl -I http://localhost:9000   # SonarQube
```

## Detener / limpiar (equivalente a rollback)

```bash
# Detener y eliminar los contenedores
docker compose down

# Detener y además borrar volúmenes y contenedores huérfanos (limpieza total)
docker compose down -v --remove-orphans
```

## Referencias

- [Documentación de Docker Compose](https://docs.docker.com/compose/).
- [Documentación de Jenkins](https://www.jenkins.io/doc/).
