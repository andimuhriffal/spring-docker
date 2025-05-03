pipeline {
    agent {
        node {
            label 'ec2-node'
        }
    }

    tools {
        git 'linux-git' // Pastikan git Linux sudah dikonfigurasi di Global Tool Configuration
    }

    environment {
        COMPOSE_FILE = 'docker-compose.yml'
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/andimuhriffal/spring-docker.git'
            }
        }

        stage('Build and Run Containers') {
            steps {
                script {
                    sh '''
                    echo "[1] Stopping any running containers..."
                    docker-compose down || true
                    
                    echo "[2] Building Docker images..."
                    docker-compose build
                    
                    echo "[3] Starting containers..."
                    docker-compose up -d
                    '''
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
        success {
            echo '✅ Deployment berhasil!'
        }
        failure {
            echo '❌ Deployment gagal. Silakan cek log.'
        }
    }
}
