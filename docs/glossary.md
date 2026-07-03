# Glosario

Vocabulario compartido del dominio y del proyecto. Mantén las definiciones cortas
y sin ambigüedad para que todo el equipo use los términos de la misma forma.

| Término            | Definición                                                                                     |
| ------------------ | ---------------------------------------------------------------------------------------------- |
| Análisis estático  | Revisión del código sin ejecutarlo, en busca de bugs, code smells y vulnerabilidades.          |
| CI                 | Integración Continua: integrar y verificar cada cambio de forma automática y frecuente.        |
| Docker Compose     | Herramienta que orquesta varios contenedores (aquí, Jenkins y SonarQube) con un solo archivo.  |
| Jenkinsfile        | Archivo que define el pipeline declarativo de Jenkins y sus stages.                            |
| JUnit              | Framework de pruebas unitarias para Java; el proyecto usa JUnit 4.                             |
| Maven              | Herramienta de build de Java que compila, gestiona dependencias y ejecuta los tests.           |
| Pipeline           | Secuencia automatizada de etapas (build, test, análisis) que corre ante cada cambio.           |
| POM                | `pom.xml`, archivo de configuración de Maven con dependencias y plugins del proyecto.          |
| Quality Gate       | Conjunto de condiciones de calidad de SonarQube que un análisis debe cumplir para aprobarse.   |
| SonarQube          | Servidor de análisis estático que mide y reporta la calidad del código.                        |
| Stage              | Cada etapa del pipeline de Jenkins (p. ej. "Build y Test" o "SonarQube Analysis").             |
| Token de análisis  | Credencial que autoriza a Jenkins/Maven a enviar resultados de análisis a SonarQube.           |

> Convención: ordena los términos alfabéticamente y enlaza al documento donde se
> detalla cada concepto cuando aplique.
