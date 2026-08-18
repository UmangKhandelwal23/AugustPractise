pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker')
        IMAGE_NAME = "umangkhandelwal/blog-frontend:v1"
    }


    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                url: 'https://github.com/UmangKhandelwal23/AugustPractise'
            }
        }

        stage('Build & Deploy') {
            steps {
                sh '''
                    cd Blog
                    docker compose up -d --build
                '''
            }
        }
        stage('Docker Push') {
            steps {
                sh """
                echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin
                docker push ${IMAGE_NAME}
                """
            }
        }

        stage('Verify') {
            steps {
                sh 'docker ps'
            }
        }
    }
}
