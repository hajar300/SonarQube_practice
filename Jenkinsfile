pipeline {
    agent any

    tools {
        jdk 'jdk-11'       // Doit correspondre au nom défini dans Jenkins > Global Tool Configuration
        maven 'Maven3'     // Idem ici pour Maven
    }

    environment {
        // Configuration de SonarQube (assure-toi que le nom correspond à celui dans Jenkins > Manage Jenkins > Configure System)
        SONARQUBE_ENV = 'SonarQube'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/hajar300/SonarQube_practice.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn clean install sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            // Ignore l'erreur si aucun rapport n'existe
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}
