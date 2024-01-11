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
                 script{

                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? "simpleapp-snapshot" : "simpleapp-release"
                nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-app', 
                            classifier: '', 
                            file: 'target/simple-app-3.0.5.war', 
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
    

