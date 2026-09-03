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

        stage('Build - UserFront') {
            steps {
                dir('UserFront') {
                    sh '/usr/bin/mvn clean package -DskipTests'
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
                sh 'docker rm -f banking-userfront banking-adminportal || true'

                sh 'docker compose up -d --no-deps userfront adminportal'
            }
        }
    }

    post {
        success {
            echo 'Pipeline termine avec succes : build et deploiement OK.'
        }
        failure {
            echo 'Le pipeline a echoue. Verifie les logs ci-dessus.'
        }
    }
}
