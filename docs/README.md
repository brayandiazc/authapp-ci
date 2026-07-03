# Documentación de AuthApp CI

Mapa de la documentación del proyecto. Empieza por aquí para saber qué documento
responde cada pregunta.

| Documento                                                      | Pregunta que responde                | Cuándo leerlo                     |
| -------------------------------------------------------------- | ------------------------------------ | --------------------------------- |
| [`architecture/architecture.md`](architecture/architecture.md) | ¿Cómo está construido el sistema?    | Al entender el panorama general   |
| [`architecture/stack.md`](architecture/stack.md)               | ¿Con qué tecnologías y versiones?    | Al configurar el entorno          |
| [`architecture/auth.md`](architecture/auth.md)                 | ¿Cómo se entra y qué se permite?     | Al tocar autenticación/permisos   |
| [`conventions/`](conventions/README.md)                        | ¿Cómo trabajamos en este repo?       | Antes de escribir código          |
| [`conventions/testing.md`](conventions/testing.md)             | ¿Cómo probamos el código?            | Al escribir o revisar pruebas     |
| [`conventions/quality-tooling.md`](conventions/quality-tooling.md) | ¿Qué herramientas de calidad usamos? | Al configurar SonarQube y linting |
| [`conventions/deploy.md`](conventions/deploy.md)               | ¿Cómo se despliega y opera?          | Al preparar un despliegue         |
| [`conventions/secrets.md`](conventions/secrets.md)             | ¿Cómo gestionamos credenciales?      | Al manejar tokens y secretos      |
| [`product/roadmap.md`](product/roadmap.md)                     | ¿Hacia dónde va?                     | Para conocer prioridades          |
| [`decisions/`](decisions/README.md)                            | ¿Por qué tomamos cada decisión?      | Antes de re-debatir algo          |
| [`glossary.md`](glossary.md)                                   | ¿Qué significa cada término?         | Ante vocabulario desconocido      |

## Sobre la distinción `architecture/` vs `conventions/`

- **`architecture/`** describe **este** proyecto en concreto (su modelo de datos, su
  auth, su API).
- **`conventions/`** describe **reglas reusables** de cómo trabajamos
  (cómo modelamos datos, cómo autenticamos, cómo testeamos) — transversales a
  cualquier feature.

## Cómo mantener esta documentación

- Actualiza la línea **"Última actualización"** al editar un documento.
- Registra las decisiones relevantes como [ADRs](decisions/README.md).
- Mantén este índice al día si agregas o quitas documentos.
