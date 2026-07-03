# AuthApp CI — Arquitectura

> Vista de alto nivel de cómo está construido el sistema de CI/CD y cómo se
> reparten las responsabilidades. Para el stack real (versiones, librerías) ver
> [`stack.md`](stack.md). Para el negocio ver
> [`../product/business-model.md`](../product/business-model.md).
>
> **Última actualización**: 2026-07-02

## Diagrama

```mermaid
graph TD
    subgraph GitHub
        A[Repositorio Git<br/>authapp-ci]
    end
    subgraph "Infraestructura Docker"
        B[Jenkins<br/>orquestador del pipeline]
        C[SonarQube<br/>análisis estático]
    end
    subgraph "App bajo prueba"
        D[authapp<br/>Java 21 + Maven]
    end

    A -->|push / cambio| B
    B -->|Build y Test<br/>mvn clean test| D
    B -->|SonarQube Analysis<br/>mvn sonar:sonar| C
    D -->|reporte de análisis| C
```

## Componentes

| Componente        | Responsabilidad                                                              | Tecnología              |
| ----------------- | --------------------------------------------------------------------------- | ----------------------- |
| Repositorio Git   | Fuente de verdad del código; cada cambio (push) dispara el pipeline.         | GitHub                  |
| Jenkins           | Orquesta el pipeline declarativo: ejecuta el build, los tests y el análisis. | Jenkins (en Docker)     |
| SonarQube         | Recibe y muestra el análisis estático de calidad del código.                 | SonarQube LTS (Docker)  |
| App `authapp`     | Objeto del build; app Java/Maven trivial que se compila y testea.           | Java 21 + Maven         |

## Decisiones clave

| Decisión                                | Razón                                                                            |
| --------------------------------------- | -------------------------------------------------------------------------------- |
| Jenkins y SonarQube en Docker Compose   | Entorno reproducible y aislado, fácil de levantar para fines educativos.         |
| Pipeline en dos stages (Build/Test y Sonar) | Separa la verificación funcional (tests) del control de calidad (análisis estático). |

> El detalle y las alternativas de cada decisión relevante se registran como
> ADRs en [`../decisions/`](../decisions/README.md).

## Reglas no negociables

- Todo cambio en GitHub debe pasar por el pipeline antes de considerarse válido.
- El stage de Build y Test debe compilar y ejecutar `mvn clean test` sin fallos.

## Flujos principales

```mermaid
sequenceDiagram
    actor Dev as Desarrollador
    participant GH as GitHub
    participant J as Jenkins
    participant M as Maven / JUnit
    participant S as SonarQube
    Dev->>GH: push de un cambio
    GH->>J: dispara el job del pipeline
    J->>M: Stage "Build y Test" (mvn clean test)
    M-->>J: resultado de compilación y pruebas
    J->>S: Stage "SonarQube Analysis" (mvn sonar:sonar)
    S-->>J: análisis de calidad
```

## Referencias

- [`stack.md`](stack.md) — stack tecnológico y versiones.
- [`auth.md`](auth.md) — autenticación (demo) de la app bajo prueba.
- [`../conventions/`](../conventions/README.md) — convenciones de trabajo.
