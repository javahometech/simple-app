pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                 nexusArtifactUploader artifacts: [
                     [
                         artifactId: 'simple-app', 
                         classifier: '', 
                         file: 'target/simple-app-1.0.0.war', 
                         type: 'war'
                    ]
                ], 
                credentialsId: 'nexus3', 
                groupId: 'in.javahome', 
                nexusUrl: '172.31.15.204:8081', 
                nexusVersion: 'nexus2', 
                protocol: 'http', 
                repository: 'http://13.233.71.181:8081/repository/simpleapp-release', 
                version: '1.0.0'
            }
        }
    }
}