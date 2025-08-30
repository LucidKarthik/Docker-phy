pipeline {
    agent any

    environment {
        IMAGE_NAME = 'luciddockerkk/flask-app'              
        DOCKER_CREDENTIALS = credentials('docker-phy')  
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'dev', url: 'https://github.com/LucidKarthik/Docker-phy.git
' 
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Login to Docker Hub') {
            steps {
                sh '''
                    echo "${DOCKER_CREDENTIALS_PSW}" | docker login -u "${DOCKER_CREDENTIALS_USR}" --password-stdin
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${IMAGE_NAME}"
            }
        }

        stage('Logout from Docker Hub') {
            steps {
                sh 'docker logout'
            }
        }
    }
}

