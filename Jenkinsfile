pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh ' docker build -t pavanvc/pythonapp:$BUILD_NUMBER .'
            }
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh ' docker push pavanvc/pythonapp:$BUILD_NUMBER'
            }
        }
    }
 post {
        success {
            emailext body: 'Your pipeline has completed successfully.',
                     subject: 'Pipeline Success Notification',
                     to: 'pavanvc347@gmail.com'
        }
        failure {
            emailext body: 'Your pipeline has failed.',
                     subject: 'Pipeline Failure Notification',
                     to: 'pavanvc347@gmail.com'
        }
    }
}

