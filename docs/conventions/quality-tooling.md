# Convenciones de calidad y tooling

> Análisis estático y calidad de código de AuthApp CI.
> **Última actualización**: 2026-07-02

## Stack

- **Análisis estático / calidad**: SonarQube (`sonarqube:lts`, en Docker, puerto 9000). Es la herramienta central de calidad del proyecto: ejecuta análisis estático y aplica un **quality gate**.
- **Linter / formateador (Java)**: no configurado formalmente. A futuro se pueden añadir Checkstyle o Spotless al `pom.xml`.
- **Auditoría de dependencias**: no configurada. Opción a futuro: OWASP Dependency-Check (`dependency-check-maven`).
- **Orquestador de git hooks**: no se usa. La verificación de calidad ocurre en la CI (Jenkins), no en hooks locales.

## Cómo se ejecuta el análisis

El análisis de calidad corre en la CI, en el stage **SonarQube Analysis** del `Jenkinsfile`, después de que pasan build y tests. El comando es:

```bash
cd authapp && mvn sonar:sonar \
  -Dsonar.projectKey=authapp \
  -Dsonar.host.url=http://sonarqube:9000
```

> El token de análisis (`sonar.login`) **no** debe ir en este comando ni en el
> repositorio; se gestiona como secreto. Ver [`secrets.md`](secrets.md).

## Reglas

- El análisis de SonarQube se ejecuta ante cada cambio, tras compilar y testear.
- Los checks de calidad se consideran **bloqueantes**: el quality gate de SonarQube debe pasar.
- Linter/formateador y auditoría de dependencias aún no están configurados; cuando se añadan, deben integrarse también en la CI.

## Comandos útiles

```bash
# Análisis de calidad (requiere SonarQube levantado y el token como secreto)
cd authapp && mvn sonar:sonar -Dsonar.projectKey=authapp -Dsonar.host.url=http://sonarqube:9000
```

> No hay comandos de lint, formato ni auditoría de dependencias porque esas
> herramientas todavía no están configuradas en el proyecto.

## Referencias

- [Documentación de SonarQube](https://docs.sonarsource.com/sonarqube/).
- [SonarScanner for Maven](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/).
