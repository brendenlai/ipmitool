node {
	git url: 'https://github.com/brendenlai/ipmitool.git'
	def server
	def uploadSpec 
	def buildInfo1
    agent any 
    
        
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
			server = Artifactory.server SERVER_ID

			// Read the upload spec which was downloaded from github.
			uploadSpec = readFile 'resources/ipmitool-upload.json'
			// Upload to Artifactory.
			buildInfo1 = server.upload spec: uploadSpec       
			// Publish the build to Artifactory
			server.publishBuildInfo buildInfo1
		}
	}
   
}
