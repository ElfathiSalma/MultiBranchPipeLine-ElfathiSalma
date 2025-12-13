pipeline {
    agent {
        docker {
            image 'my-maven-git:latest'
            // Utiliser un volume Docker pour Maven plutôt que $HOME
            args '-v maven-repo:/root/.m2'
        }
    }
    options {
        // Supprime le workspace automatiquement avant chaque build
        skipDefaultCheckout(false)
    }
    stages {
        stage('Checkout') {
            steps {
                // Nettoyer le workspace proprement
                deleteDir()
                
                // Checkout avec les credentials Jenkins configurés
                checkout scm
            }
        }
        stage('Build & Test') {
            steps {
                script {
                    echo "Current directory: ${pwd()}"
                    
                    // Run Maven commands à la racine du repo
                    sh 'mvn clean test package'
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    // Exécuter le jar généré
                    sh 'java -jar target/maven-0.0.1-SNAPSHOT.jar'
                }
            }
        }
    }
}
