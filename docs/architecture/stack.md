# Stack Tecnológico

> Fuente de verdad de las tecnologías y versiones del proyecto.
> **Última actualización**: 2026-07-02

## Runtime y aplicación

| Categoría      | Tecnología | Versión | Por qué                                                                 |
| -------------- | ---------- | ------- | ----------------------------------------------------------------------- |
| Runtime        | Java       | 21      | Lenguaje de la app demo bajo prueba; versión LTS moderna.               |
| Build / gestor | Maven      | 3.x     | Compila, resuelve dependencias y ejecuta el ciclo de test del proyecto. |

## Testing

| Categoría | Tecnología | Versión | Por qué                                                            |
| --------- | ---------- | ------- | ----------------------------------------------------------------- |
| Testing   | JUnit      | 4       | Framework de pruebas unitarias que corre el pipeline en cada push. |

## DevOps & Herramientas

| Categoría            | Tecnología             | Versión | Por qué                                                                   |
| -------------------- | ---------------------- | ------- | ------------------------------------------------------------------------- |
| CI/CD                | Jenkins (en Docker)    | LTS     | Orquesta el pipeline declarativo (build, test y análisis) en cada cambio. |
| Contenedores         | Docker + Docker Compose| —       | Levanta Jenkins y SonarQube de forma reproducible y aislada.              |
| Análisis de calidad  | SonarQube              | lts     | Análisis estático de código y control de calidad del proyecto.            |

## Justificación de elecciones

| Tecnología elegida     | Alternativa descartada | Razón                                                                                   |
| ---------------------- | ---------------------- | --------------------------------------------------------------------------------------- |
| Jenkins (self-hosted)  | GitHub Actions         | El objetivo educativo es aprender a operar un CI/CD self-hosted, no un runner gestionado. |
| SonarQube self-hosted  | SonarCloud (SaaS)      | Se busca entender el despliegue y la administración del propio servidor de calidad.      |

## Versiones mínimas soportadas

- Java >= 21
- Maven >= 3.8
- SonarQube >= lts
