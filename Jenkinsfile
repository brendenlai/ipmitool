pipeline {
    agent any 
    stages {
        
        stage('Build') { 
            steps {
                // 
                sh "echo building .... "
                sh "./configure"
                sh "autoreconf -ivf"
                sh "make"
            }
        }
        stage('Deploy') { 
            steps {
                // 
                sh "echo Deploying .... "
                def server = Artifactory.server SERVER_ID

				// Read the upload spec which was downloaded from github.
				def uploadSpec = readFile 'resources/ipmitool-upload.json'
				// Upload to Artifactory.
				def buildInfo1 = server.upload spec: uploadSpec       
				// Publish the build to Artifactory
				server.publishBuildInfo buildInfo1
            }
        }
    }
}
