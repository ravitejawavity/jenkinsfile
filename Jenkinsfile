def server = Artifactory.server 'Artifactory'
def rtGradle = Artifactory.newGradleBuild()
pipeline {
    agent any

    stages {
        stage ('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/jitpack/gradle-simple.git"
            }
        }

        stage ('Upload') {
            steps {
                rtUpload (
                    buildName: 'holyFrog',
                    buildNumber: '42',
                    serverId: 'Artifactory Version 4.15.0', // Obtain an Artifactory server instance, defined in Jenkins --> Manage:
                    specPath: 'gradle-dev-local/com.github.jitpack/artifactory-integration/recursive-flat-upload.json'                   
                )
            }
        }

        stage ('Download') {
            steps {
                rtDownload (
                    buildName: 'holyFrog',
                    buildNumber: '42',
                    serverId: 'Artifactory Version 4.15.0',
                    specPath: 'gradle-dev-local/com.github.jitpack/artifactory-integration/aql-download.json'
                )
            }
        }

        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    buildName: 'holyFrog',
                    buildNumber: '42',
                    serverId: 'Artifactory Version 4.15.0'
                )
            }
        }
    }
}
