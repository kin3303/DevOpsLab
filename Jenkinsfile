pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                script {
                
				def pom = readMavenPom file: 'pom.xml'
				def ArtifactId = ${pom.artifactId}
				def Version = ${pom.version}
				def Name = ${pom.name}
				def GroupId = ${pom.groupId}
                def NexusRepo = Version.endsWith("SNAPSHOT") ? "DevOpsLab-SNAPSHOT" : "DevOpsLab-RELEASE"

                nexusArtifactUploader artifacts: [[artifactId: "${ArtifactId}", classifier: '', file: "target/${ArtifactId}-${Version}.war", type: 'war']], 
                credentialsId: '35e9b26e-269a-4804-a70d-6b2ec7a608ce', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.140:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
             }
            }
        }
    }

}
