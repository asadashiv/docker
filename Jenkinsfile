pipeline {
    agent {label 'slave_docker'}
    parameters {
  credentials credentialType: 'com.cloudbees.plugins.credentials.impl.UsernamePasswordCredentialsImpl', defaultValue: 'docker', name: 'DOCKERHUB', required: false
}
    stages { 
        stage('clone') {
            steps{
            git branch: 'main', url: 'https://github.com/asadashiv/docker.git'
            }
        }

        stage('Build-image') {
            steps {  
                sh 'sudo docker build -t shivasada/project .'
            }
        }
        stage('login') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'sudo docker push shivasada/project'
            }
        }
        stage('build container') {
            steps{
                sh 'sudo docker run -d -p 81:80 shivasada/project'
            }
        }
    }        
}
