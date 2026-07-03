pipeline {
  agent any

  tools {
    jdk 'Java21'
    maven 'Maven3'
  }

  environment {
    SONARQUBE_ENV = 'SonarQube'
    // Token de análisis leído desde una credencial de Jenkins (tipo "Secret text").
    // Créala en: Manage Jenkins > Credentials, con el ID 'sonar-token'.
    // Nunca hardcodees el token en este archivo. Ver docs/conventions/secrets.md.
    SONAR_TOKEN = credentials('sonar-token')
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
        dir('authapp') {
          withSonarQubeEnv("${SONARQUBE_ENV}") {
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
