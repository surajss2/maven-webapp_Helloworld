pipeline {
    agent any
    tools{
        maven 'M2_MAVEN'
    }
     
    stages {
        stage('clean the project') {
            steps {
                sh 'mvn clean'
            }
        }
        stage("Build the project"){
            steps {
                sh ' mvn install package'
            }
            post {
                success {
                    echo "Archieving the Artifact"
                    archiveArtifacts Artifacts: '**/target/*.war'
                }
                }
        }
        stage("deploying stage"){
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
