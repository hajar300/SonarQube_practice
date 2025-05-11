pipeline {
    agent any

    tools {
        jdk 'jdk-11'       // Nom défini dans Jenkins > Global Tool Configuration
        maven 'Maven3'     // Nom défini dans Jenkins > Global Tool Configuration
    }

    environment {
        SONARQUBE_ENV = 'SonarQube'   // Nom du serveur SonarQube configuré dans Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/hajar300/SonarQube_practice.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                        sh 'mvn clean install sonar:sonar -Dsonar.login=$SONAR_TOKEN'
                    }
                }
            }
        }
    }

    post {
        always {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}
