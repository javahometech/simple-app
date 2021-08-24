pipeline {
  agent any
    tools{
        jdk 'java'
        maven 'maven'
    }
  
  stages {
     stage('CleanWorkspace') {
            steps {
                cleanWs()
            }
        }       
      stage("Code Checkout"){
            steps {
                script {
                                                                
                    sh "git clone https://github.com/mhali922/simple-app.git"
                   
}
}
}
            stage('Build'){
            steps{
                script{
                 sh "cp -rp $workspace/simple-app/* $workspace";
                 sh "mvn clean package";
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{

                    def mavenPom = readMavenPom file: 'pom.xml'
                    def nexusRepoName = mavenPom.version.endsWith("SNAPSHOT") ? 'simpleapp-snapnot' : 'simpleapp-release'
                    nexusArtifactUploader artifacts: [
                        [
                            artifactId: 'simple-app', 
                            classifier: '', 
                            file: "target/simple-app-${mavenPom.version}.war", 
                            type: 'war'
                        ]
                    ], 
                    credentialsId: 'nexus3', 
                    groupId: 'in.javahome', 
                    nexusUrl: '172.31.23.232:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: nexusRepoName, 
                    version: "${mavenPom.version}"
                    }
            }
        }
    }
}
