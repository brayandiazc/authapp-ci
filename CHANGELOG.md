# Changelog

Todos los cambios notables de este proyecto se documentan en este archivo.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/)
y este proyecto adhiere a [Semantic Versioning](https://semver.org/lang/es/).

## [Unreleased]

### Added

### Changed

### Deprecated

### Removed

### Fixed

### Security

## [1.0.0] - 2026-07-02

### Added

- Pipeline de CI con **Jenkins** (declarativo, en Docker): stages de _Build y Test_ y _SonarQube Analysis_.
- Análisis estático de código con **SonarQube** (Docker, imagen `sonarqube:lts`).
- Orquestación de servicios con **Docker Compose** (Jenkins + SonarQube).
- Aplicación de ejemplo `authapp` (Java 21 + Maven) con pruebas **JUnit 4**.
- Estructura de documentación completa en [`docs/`](docs/README.md): arquitectura, convenciones, decisiones (ADR) y roadmap.
- Archivos de gobernanza del repositorio: `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `.editorconfig`, `.env.example`.
- Plantillas de issues y Pull Requests, configuración de Dependabot y automatización de labels en [`.github/`](.github).

### Security

- Documentada la política de manejo de secretos: el token de análisis de SonarQube debe gestionarse con Jenkins Credentials y nunca commitearse (ver [`docs/conventions/secrets.md`](docs/conventions/secrets.md)).

<!--
Enlaces de comparación entre versiones:
[Unreleased]: https://github.com/brayandiazc/authapp-ci/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/brayandiazc/authapp-ci/releases/tag/v1.0.0
-->
