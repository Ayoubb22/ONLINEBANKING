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

        stage('Diagnostic') {
            steps {
                sh 'echo PATH=$PATH'
                sh 'which mvn || echo "mvn not in PATH"'
                sh 'ls -la /usr/bin/mvn || echo "no /usr/bin/mvn"'
                sh '/usr/bin/mvn -version || echo "absolute path failed too"'
            }
        }

        stage('Build & Test - UserFront') {
            steps {
                dir('UserFront') {
                    sh '/usr/bin/mvn clean package'
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
