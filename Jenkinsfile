pipeline {
    agent any
    tools {
        maven M2_MAVEN 
        }
      
    stages {
        stage(' project build') {
            steps {
                sh 'mvn clean install package'
            }
        }
        stage("Push the docker image to docker Hub"){
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'my-app', 
                        classifier: '', 
                        file: '/var/lib/jenkins/workspace/Jenkins-nexus-project/target/*.war', 
                        type: 'war'
                    ]
                ], 
                credentialsId: 'nexus', 
                groupId: 'com.dme.app', 
                nexusUrl: '192.168.30.142:8081', 
                nexusVersion: 'nexus3', protocol: 'http',
                repository: 'simpleapp-maven', version: '3.0-SNAPSHOT'
            }
        }
        
                        
    }
    
}
