pipeline {
    agent any

    environment {
        IMAGE_NAME = "springboot-docker-jenkin-demo"
        CONTAINER_NAME = "springboot-docker-jenkin-demo-container"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/anjaneyulu1013/docker-jenkins-demo.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh 'chmod +x mvnw'
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop $CONTAINER_NAME || true
                docker rm $CONTAINER_NAME || true
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker run -d \
                -p 8081:8080 \
                --name $CONTAINER_NAME \
                $IMAGE_NAME
                '''
            }
        }
    }
}