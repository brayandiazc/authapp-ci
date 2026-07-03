# 📌 AuthApp CI

Pipeline de integración continua para una aplicación Java utilizando Jenkins, Maven y SonarQube. El proyecto analiza el código automáticamente con cada cambio en GitHub, compila, ejecuta pruebas y envía los resultados a SonarQube para revisión de calidad.

![Build](https://img.shields.io/badge/build-Jenkins-D24939?logo=jenkins&logoColor=white)
![Java](https://img.shields.io/badge/Java-21-007396?logo=openjdk&logoColor=white)
![Quality](https://img.shields.io/badge/quality-SonarQube-4E9BCD?logo=sonarqube&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue)

## 🧱 Composición del Proyecto

- 🔧 **Java 21** — Código fuente de la app (`/authapp`)
- ⚙️ **Maven** — Build y ejecución de pruebas
- 🚀 **Jenkins (Docker)** — Automatiza el proceso CI/CD
- 📊 **SonarQube (Docker)** — Análisis estático de código
- 🐳 **Docker Compose** — Orquestación de servicios

> ℹ️ La app `authapp` es un **demo educativo** de autenticación en memoria. Su único fin es dar algo real que compilar y testear en el pipeline; no es un sistema de autenticación de producción. Ver [`docs/architecture/auth.md`](docs/architecture/auth.md).

## 🖼️ Vista Previa

| Jenkins                     | SonarQube                       |
| --------------------------- | ------------------------------- |
| ![jenkins](img/jenkins.png) | ![sonarqube](img/sonarqube.png) |

## ⚙️ Requisitos

- Docker
- Docker Compose
- Git

## 🚀 Instalación

```bash
# Clona el repositorio
git clone https://github.com/brayandiazc/authapp-ci.git
cd authapp-ci

# Asegúrate de tener esta estructura:
# .
# ├── docker-compose.yml
# ├── jenkins/
# │   └── Dockerfile
# └── authapp/
#     └── (código Java + pom.xml)

# Construye y levanta los contenedores
docker compose up --build -d

# Extrae la contraseña inicial de Jenkins
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

## 🔐 Configuración de Jenkins

1. Accede a [http://localhost:8080](http://localhost:8080)

2. Ingresa la contraseña inicial (ver paso anterior)

3. Instala los plugins sugeridos

4. Configura las herramientas:

   - **Java 21** (verifica con `readlink -f $(which java)`)
   - **Maven 3.x** (`/usr/share/maven`)
   - **SonarQube**:

     - Nombre: `SonarQube`
     - URL: `http://sonarqube:9000`

5. Agrega un nuevo _Pipeline Job_:

   - Origen: Git → `https://github.com/brayandiazc/authapp-ci.git`
   - Branch: `main`
   - Script Path: `Jenkinsfile`

## 📄 Jenkinsfile

```groovy
pipeline {
  agent any

  tools {
    jdk 'Java21'
    maven 'Maven3'
  }

  environment {
    SONARQUBE_ENV = 'SonarQube'
  }

  stages {
    stage('Build y Test') {
      steps {
        dir('authapp') {
          sh 'mvn clean test'
        }
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv("${SONARQUBE_ENV}") {
          dir('authapp') {
            sh '''
              mvn sonar:sonar \
                -Dsonar.projectKey=authapp \
                -Dsonar.host.url=http://sonarqube:9000 \
                -Dsonar.login=$SONAR_TOKEN
            '''
          }
        }
      }
    }
  }
}
```

🔐 **Importante**: genera tu token en SonarQube (`http://localhost:9000 > My Account > Security > Generate Tokens`) y **nunca lo hardcodees** en el `Jenkinsfile`. Guárdalo como credencial de Jenkins (_Manage Jenkins → Credentials_, tipo _Secret text_) y referéncialo. Ver [`docs/conventions/secrets.md`](docs/conventions/secrets.md).

## 🧪 Pruebas

El sistema ejecuta automáticamente `mvn clean test` dentro del pipeline CI. Para ejecutarlas en local:

```bash
cd authapp
mvn clean test
```

Convenciones de testing en [`docs/conventions/testing.md`](docs/conventions/testing.md).

## 🛑 Parar el entorno

```bash
docker compose down
```

Para limpiar todo:

```bash
docker compose down -v --remove-orphans
```

## 🛣️ Roadmap

- [x] Jenkins con Maven
- [x] Análisis con SonarQube
- [ ] Notificaciones Slack
- [ ] Despliegue automático (CD)

Roadmap detallado en [`docs/product/roadmap.md`](docs/product/roadmap.md).

## 📚 Documentación

Toda la documentación vive en [`docs/`](docs/README.md):

| Documento                                                                | Responde a                        |
| ------------------------------------------------------------------------ | --------------------------------- |
| [`docs/architecture/architecture.md`](docs/architecture/architecture.md) | ¿Cómo está construido el pipeline? |
| [`docs/architecture/stack.md`](docs/architecture/stack.md)               | ¿Con qué tecnologías?             |
| [`docs/architecture/auth.md`](docs/architecture/auth.md)                 | ¿Qué hace la app de ejemplo?      |
| [`docs/conventions/`](docs/conventions/README.md)                        | ¿Cómo trabajamos en este repo?    |
| [`docs/decisions/`](docs/decisions/README.md)                            | ¿Por qué tomamos cada decisión?   |
| [`docs/product/roadmap.md`](docs/product/roadmap.md)                     | ¿Hacia dónde va?                  |

## 🖇️ Contribuye

Lee la [Guía de Contribución](CONTRIBUTING.md) para conocer el flujo de trabajo (Git Flow), el formato de commits (Conventional Commits) y el proceso de Pull Requests. Al participar, aceptas el [Código de Conducta](CODE_OF_CONDUCT.md).

## 🔒 Seguridad

¿Encontraste una vulnerabilidad? Revisa la [Política de Seguridad](SECURITY.md) antes de reportarla.

## 🏷️ Versionado

Seguimos [Semantic Versioning](https://semver.org/lang/es/). Consulta las [versiones publicadas](https://github.com/brayandiazc/authapp-ci/tags) y el [CHANGELOG](CHANGELOG.md).

## 📄 Licencia

MIT — ver [LICENSE](LICENSE)

⌨️ con ❤️ por [Brayan Diaz C](https://github.com/brayandiazc)
