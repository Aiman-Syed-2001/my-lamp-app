pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.test.yml'
        DEPLOYMENT_URL = 'http://13.60.215.94'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/Aiman-Syed-2001/my-lamp-app.git'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker-compose -f $DOCKER_COMPOSE_FILE up --build --abort-on-container-exit'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'tests/report.html', allowEmptyArchive: true
        }
        
        success {
            echo "✅ Deployment is live at: $DEPLOYMENT_URL"
        }

        failure {
            echo "❌ Build failed. Please check the logs and test report."
        }
    }
}
