pipeline {
    agent any

    environment {
        DOCKER_COMPOSE_FILE = 'docker-compose.test.yml'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/Aiman-Syed-2001/my-lamp-app.git'
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
    }
}
