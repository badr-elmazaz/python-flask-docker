pipeline {
    agent { 
        label 'docker-builder'
      }
      environment {
        DOCKERHUB_CREDENTIALS = credentials('DOCKERHUB_CREDENTIALS')
      }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                docker build -t badrelmazaz/test-image:latest .
                '''
            }
        }
        stage('Login') {
            steps {
                echo "Logging in.."
                sh '''
                docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW
                '''
            }
        }
        stage('Push') {
            steps {
                echo 'Pushing image....'
                sh '''
                docker push badrelmazaz/test-image:latest
                '''
            }
        }
    }
    post {
        always {
            echo 'Logging out..'
            sh '''
            docker logout
            '''
        }
    }
}
