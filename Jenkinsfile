pipeline {
    agent any
    tools {
        maven 'maven1'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                        [
                            artifactId: '**/target/*.war', 
                            classifier: '', 
                            file: '', 
                            type: 'war'
                        ]
                    ], 
                  credentialsId: 'Nexus3', 
                  groupId: 'in.javahome', 
                  nexusUrl: '172.31.7.89:8081', 
                  nexusVersion: 'nexus3', 
                  protocol: 'http', 
                  repository: 'testrepo', 
                  version: '3.0.5'
               }
            }
        }
   }
    

