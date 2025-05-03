pipeline {
    agent {
        node {
            label 'ec2-node'
        }
    }

    tools {
        git 'Default'
    }

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {
        stage('Build and Run Containers') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose build'
                    sh 'docker-compose up -d'
                }
            }
        }

        stage('Verify Containers') {
            steps {
                sh 'docker-compose ps'
            }
        }
    }

    post {
        always {
            echo 'Pipeline telah selesai dijalankan di node ec2-node.'
        }
    }
}
