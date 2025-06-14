pipeline {
    agent any
    environment {
        COMPOSE_PROJECT_NAME = 'rediscluster'
    }
    stages {
        stage('Build Sentinel Image') {
            steps {
                sh 'docker compose build sentinel'
            }
        }
        stage('Start Cluster') {
            steps {
                sh 'docker compose up -d --remove-orphans || true'
                sh 'docker compose up -d'
            }
        }
        stage('Verify Cluster') {
            steps {
                sh 'sleep 10'
                sh 'docker compose ps'
                sh './test.sh || true'
            }
        }
    }
    post {
        always {
            sh 'docker compose down --remove-orphans'
        }
    }
}
