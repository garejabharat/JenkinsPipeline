pipeline{
    agent any
    tools {nodejs "node"}
    environment{
        imageName =  "techwithbk/jenkins_app" 
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
                 dockerImage = docker.build imageName
               }
            }
       }

                }       stage("Deploy Image"){
            steps{
               script{
                docker.withRegistry ("https://index.docker.io/v1/",rigistryCredential){
                    dockerImage.push("${env.BUILD_NUMBER}") 
               }
            }
       }
    }
}   

