pipeline {
    agent {
        node {
            label 'ec2-node'
        }
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/andimuhriffal/spring-docker.git']]])
            }
        }

        stage('Build and Run Containers') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose build'
                sh 'docker-compose up -d'
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
