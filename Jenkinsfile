pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                dir('maven') {
                    bat 'mvn clean package'
                }
            }
        }
    }
}
