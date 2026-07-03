# Roadmap — AuthApp CI

> Estado y dirección del producto. Documento vivo.
> **Última actualización**: 2026-07-02

## Leyenda

- ✅ Hecho
- 🚧 En curso
- 📋 Planificado
- ⏸️ Diferido

## Visión

AuthApp CI es un proyecto educativo cuyo objetivo es construir, paso a paso, un
pipeline de CI/CD self-hosted y reproducible. A largo plazo se busca que cada
push dispare de forma automática compilación, pruebas, análisis de calidad y,
finalmente, notificaciones y despliegue continuo, usando herramientas estándar
de la industria (Jenkins, SonarQube, Docker).

## Estado actual

Hoy el pipeline compila y prueba una app Java/Maven trivial (`/authapp`) y
ejecuta análisis estático con SonarQube en cada push. Todo el entorno (Jenkins y
SonarQube) se levanta con Docker Compose de forma reproducible. La app existe
únicamente para dar algo que compilar y testear; el foco del proyecto es el
pipeline, no la aplicación.

## Por fases

### Fase 1 — CI base ✅

- [x] Pipeline de Jenkins con Maven (compila y ejecuta pruebas JUnit en cada push).
- [x] Análisis de calidad con SonarQube integrado en el pipeline.
- [x] Orquestación del entorno (Jenkins + SonarQube) con Docker Compose.

### Fase 2 — Calidad y hardening (corto plazo) 🚧

- [ ] 🚧 Migrar el token de SonarQube a Jenkins Credentials (dejar de exponerlo en texto plano).
- [ ] 📋 Cobertura de código con JaCoCo, publicada en SonarQube.
- [ ] 📋 Formateo y linting con Checkstyle / Spotless.

### Fase 3 — Notificaciones y CD (medio plazo) 📋

- [ ] 📋 Notificaciones del resultado del pipeline a Slack.
- [ ] 📋 Despliegue continuo (CD) automático tras un build verde.

## Backlog / ideas sin agendar

- Quality Gate de SonarQube que rompa el build si baja la calidad.
- Badges de estado (build / cobertura) en el README.

## Fuera de alcance

- Convertir `/authapp` en una app de autenticación real: es solo una demo en
  memoria para tener algo que compilar y testear.
- Migrar a un CI gestionado (GitHub Actions): el objetivo del proyecto es
  aprender un pipeline self-hosted con Jenkins.

## Cómo se actualiza este documento

- Revisar al cerrar cada versión/fase.
- Las decisiones que cambian el rumbo se registran como ADRs en [`../decisions/`](../decisions/README.md).
