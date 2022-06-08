pipeline{
    agent any
    stages {
        stage('Build Docker Image') {
            steps {
                sh "echo staring build the image"
                sh 'docker build -t viraj5132/gitops:${env.BUILD_NUMBER} .'
            }
        }
        stage('Deploy Docker Image') {
            steps {
                sh "echo staring deploy the image"
                sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                sh 'docker push viraj5132/gitops:${env.BUILD_NUMBER}'
            }
        }
        stage('Trigger ManifestUpdate') {
             steps {
                sh " echo triggering updatemanifestjob"
                 build job: 'updatemanifest'
             }
         }   
    }
}