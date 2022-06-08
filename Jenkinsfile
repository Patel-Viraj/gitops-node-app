pipeline{
    agent any
    stages {
        stage('Build Docker Image') {
            // steps {
            //     sh "echo staring build the image"
                // image =  docker build -t viraj5132/gitops .
                image = docker.build("viraj5132/gitops")
            // }
        }
        stage('Deploy Docker Image') {
            steps {
                sh "echo staring deploy the image"
                  docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                  image.push("${env.BUILD_NUMBER}")
        }
                // sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                // sh 'docker push viraj5132/gitops:${BUILD_NUMBER}'
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