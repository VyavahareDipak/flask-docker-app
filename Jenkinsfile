pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-app"
        CONTAINER_NAME = "flask-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/your-repo/flask-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                docker run -d -p 5000:5000 --name $CONTAINER_NAME $IMAGE_NAME
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
