pipeline {
    agent any

    environment {
        COMPOSE_PROJECT = "online-banking-with-java-spring-boot-angular-2-master"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build & Test - UserFront') {
            steps {
                dir('UserFront') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker compose build userfront adminportal'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d'
            }
        }
    }

    post {
        success {
            echo 'Pipeline termin? avec succ?s : build, tests et d?ploiement OK.'
        }
        failure {
            echo 'Le pipeline a ?chou?. V?rifie les logs ci-dessus.'
        }
    }
}
