pipeline {
    agent any

    environment {
        IMAGE_NAME = "local-node-app"
        CONTAINER_NAME = "node-app"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Deploy Locally') {
            steps {
                sh """
                  
                  docker run -d --name $CONTAINER_NAME -p 3000:3000 $IMAGE_NAME
                """
            }
        }
    }

    post {
        success {
            echo "✅ Local Deployment Successful"
        }
        failure {
            echo "❌ Pipeline Failed"
        }
    }
}
