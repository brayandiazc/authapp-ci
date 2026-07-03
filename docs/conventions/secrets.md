# Convenciones de secretos y credenciales

> Cómo gestionamos secretos en AuthApp CI.
> **Última actualización**: 2026-07-02

## Filosofía

- Los secretos **nunca** se commitean en texto plano (ni en el `Jenkinsfile`).
- Separación clara entre **configuración** (no sensible, p. ej. `sonar.projectKey`, `sonar.host.url`) y **secretos** (sensible, p. ej. el token de análisis).

## Secreto del proyecto

El único secreto actual es el **token de análisis de SonarQube** (`sonar.login`), que autoriza al pipeline a subir resultados al servidor de SonarQube.

| Secreto                   | Dónde debe vivir                                            |
| ------------------------- | ---------------------------------------------------------- |
| Token de SonarQube (`sonar.login`) | Jenkins Credentials (tipo *Secret text*), referenciado desde el job |

## Reglas

- El token de SonarQube **nunca** debe ir hardcodeado en el `Jenkinsfile` ni commitearse al repositorio.
- Debe almacenarse en **Jenkins → Manage Jenkins → Credentials** como *Secret text* y referenciarse desde el pipeline (o inyectarse como variable de entorno del job).
- Comparte secretos con nuevos colaboradores **fuera de banda** (nunca por git, email plano ni chat público).
- Rota el token periódicamente (sugerido cada 90 días) y de inmediato ante sospecha de fuga.
- Si un secreto se commitea por error: **rota el secreto primero**, luego limpia la historia.

## Estado actual (deuda técnica)

> **Atención**: hoy el token de SonarQube está **hardcodeado en texto plano en el
> `Jenkinsfile`** (parámetro `-Dsonar.login=...` del stage *SonarQube Analysis*).
> Esto es una **mala práctica** de seguridad. Acciones pendientes:
>
> 1. **Rotar** el token actual en SonarQube (ya quedó expuesto en el repositorio).
> 2. Guardar el nuevo token en **Jenkins Credentials** como *Secret text*.
> 3. Modificar el `Jenkinsfile` para referenciar la credencial en vez del valor
>    literal, y limpiar la historia de git del token expuesto.

## Cómo gestionar el secreto (vía real)

No se usa un archivo `.env`. El token se administra desde la interfaz de Jenkins:

- **Jenkins → Manage Jenkins → Credentials** → añadir credencial *Secret text* con el token.
- En el pipeline, referenciarla (por ejemplo con `withCredentials` o `credentials(...)`) e inyectarla como variable de entorno del job.

## Referencias

- [Using credentials en Jenkins](https://www.jenkins.io/doc/book/using/using-credentials/).
- [SonarQube: user tokens](https://docs.sonarsource.com/sonarqube/latest/user-guide/user-account/generating-and-using-tokens/).
