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
                            file: '', 
                            type: 'war'
                        ]
                    ], 
                  credentialsId: 'Nexus3', 
                  groupId: 'in.javahome', 
                  nexusUrl: '65.0.73.39:8081', 
                  nexusVersion: 'nexus3', 
                  protocol: 'http', 
                  repository: 'testrepo', 
                  version: '3.0.5'
               }
            }
        }
   }
}

