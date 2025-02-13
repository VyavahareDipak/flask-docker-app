pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app"
        CONTAINER_NAME = "flask-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch:'main', url:'https://github.com/VyavahareDipak/flask-docker-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t ${IMAGE_NAME} .'
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker stop ${CONTAINER_NAME} || true
                docker rm ${CONTAINER_NAME} || true
                docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}
                '''
            }
        }
    }

    post {
        success {
            echo "Flask Application Deployed Successfully!"
        }
        failure {
            echo "Build or Deployment Failed!"
        }
    }
}
