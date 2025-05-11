pipeline {
    agent any  // Utiliser un agent pour exécuter le pipeline (peut être un serveur Jenkins ou local)

    tools {
        jdk 'jdk-11'  // Utiliser le JDK 11 configuré dans Jenkins
        maven 'Maven3'  // Assurez-vous que Maven est installé et configuré dans Jenkins
    }

    stages {
        // Étape 1 : Checkout du code depuis GitHub
        stage('Checkout') {
            steps {
                git 'https://github.com/hajar300/SonarQube_practice.git'  // URL du dépôt Git
            }
        }

        // Étape 2 : Compilation du projet
        stage('Build') {
            steps {
                script {
                    // Utiliser Maven pour construire le projet et exécuter SonarQube
                    sh 'mvn clean install sonar:sonar'  // Commande pour construire et analyser le code avec SonarQube
                }
            }
        }
    }

    post {
        // Cette section est exécutée après la construction
        always {
            junit '**/target/test-*.xml'  // Récupérer les résultats des tests (si disponibles)
        }
    }
}
