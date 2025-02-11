pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Balaji-Jeyachandran/jenkins-virtual-hosting.git' 
        APP_DIR = '/var/www/jenkins-virtual-hosting' 
    }

    stages {
        stage('Clone Repository') {
            steps {
                script {
                    if (fileExists("${APP_DIR}")) {
                        sh "cd ${APP_DIR} && git pull origin main"
                    } else {
                        sh "git clone ${REPO_URL} ${APP_DIR}"
                    }
                }
            }
        }

        stage('Build & Deploy Docker Containers') {
            steps {
                script {
                    sh """
                    cd ${APP_DIR}
                    docker-compose down
                    docker-compose up -d --build
                    """
                }
            }
        }

        stage('Clean Up Old Images') {
            steps {
                script {
                    sh "docker image prune -f"
                }
            }
        }
    }
}
