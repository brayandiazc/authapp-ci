# 0002. Jenkins y SonarQube para el pipeline de CI

- **Estado**: Aceptada
- **Fecha**: 2026-07-02
- **Decisores**: Brayan Diaz C

## Contexto y problema

El proyecto necesita un pipeline de integración continua **self-hosted** y con
fines de aprendizaje que, ante cada push, compile, ejecute las pruebas y evalúe
la calidad del código de una aplicación Java/Maven. El objetivo no es la app en
sí (una demo trivial de autenticación en memoria), sino ganar experiencia con
las herramientas de CI/CD que se usan en la industria. Las restricciones son:
control total sobre el pipeline, entorno reproducible en cualquier máquina y no
depender de un servicio gestionado externo.

## Opciones consideradas

- **Jenkins + SonarQube (self-hosted, en Docker)** — orquestador clásico y
  ampliamente usado, con análisis estático dedicado; todo levantable localmente.
- **GitHub Actions** — CI gestionado e integrado con el repositorio, sin nada que
  mantener, pero no cumple el objetivo de aprender un CI self-hosted.
- **GitLab CI** — potente y self-hosted, pero atado al ecosistema GitLab.
- **Travis CI** — sencillo, pero gestionado y en declive de adopción.

## Decisión

Elegimos **Jenkins** (pipeline declarativo, ejecutándose en un contenedor Docker
en el puerto 8080) como orquestador del pipeline, y **SonarQube** (imagen
`sonarqube:lts` en Docker, puerto 9000) para el análisis estático de calidad.
Ambos servicios se levantan juntos mediante **Docker Compose**, de modo que el
entorno completo sea reproducible con un solo comando. Se eligió Jenkins por
sobre GitHub Actions precisamente porque el propósito del proyecto es aprender un
pipeline self-hosted con herramientas estándar de la industria.

## Consecuencias

**Positivas:**

- Control total sobre el pipeline en un entorno self-hosted.
- Experiencia práctica con Jenkins y SonarQube, herramientas habituales en la industria.
- Entorno reproducible y portable gracias a Docker / Docker Compose.

**Negativas / costos:**

- Solución más pesada que un CI gestionado como GitHub Actions.
- Requiere mantener y actualizar los contenedores (Jenkins, SonarQube).
- Gestión manual de credenciales (p. ej. el token de SonarQube).

**Neutras / a vigilar:**

- La gestión de secretos debería migrar a Jenkins Credentials (ver roadmap).

## Referencias

- [`0001-record-architecture-decisions.md`](0001-record-architecture-decisions.md)
- [Jenkins](https://www.jenkins.io/)
- [SonarQube](https://www.sonarsource.com/products/sonarqube/)
