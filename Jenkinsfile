pipeline {
    agent {label 'docker'}
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker')
    }
    stages { 
        stage('clone') {
            steps{
            git branch: 'main', url: 'https://github.com/asadashiv/docker.git'
            }
        }

        stage('Build-image') {
            steps {  
                sh 'docker build -t shivasada/project .'
            }
        }
        stage('login') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push shivasada/project'
            }
        }
        stage('build container') {
            steps{
                sh 'docker run -d -p 80:80 shivasada/project'
            }
        }
    }        
}
