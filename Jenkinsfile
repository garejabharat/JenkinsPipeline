pipeline{
    agent any
    tools {nodejs "node"}
    environment{
        // imageName =  "techwithbk/jenkins_app" 
        registry = "bharatgareja/docker_jenkins"
        rigistryCredential='dockerhub-creds'
        dockerImage = ''
    }
    stages {

       stage("Install Dependencies"){
            steps{  
                sh 'npm install'
            }
       }    
       stage("Tests"){
            steps{
                sh 'npm test'
            }
       }

       stage("Building Image"){
            steps{
               script{
                 dockerImage = docker.build registry + ":$BUILD_NUMBER"
               }
            }
       }

                   
    stage("Deploy Image"){
            steps{
               script{
                docker.withRegistry( '', registryCredential ) {
                    dockerImage.push()
                }
            }
       }
    }
    
    }
}   

