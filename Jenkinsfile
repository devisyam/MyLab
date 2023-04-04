pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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
        stage ('test'){
            steps {
                echo ' Testing......'

            }
        }
        stage ('nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: "${ArtifactId }", classifier: '', file: 'target/VinayDevOpsLab-0.0.8.war', type: 'war']], credentialsId: '1fefa95b-1c0e-4295-b9d1-44db1ad64aa4', groupId: "${GroupId}", nexusUrl: '192.168.33.29:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'devisyam-SNAPSHOT', version: "${Version}"
            } 
       }
        stage ('Print Environment variables'){
                  steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                  }
        }
    }
}
