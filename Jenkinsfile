node {
	
	def server = Artifactory.server SERVER_ID;
	def uploadSpec 
	def buildInfo1
    agent any 
    
    stage('Clone'){ 
		steps {
			// 
			git url: 'https://github.com/brendenlai/ipmitool.git'
		}
	}
        
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
			

			// Read the upload spec which was downloaded from github.
			uploadSpec = readFile 'resources/ipmitool-upload.json'
			// Upload to Artifactory.
			buildInfo1 = server.upload spec: uploadSpec       
			// Publish the build to Artifactory
			server.publishBuildInfo buildInfo1
		}
	}
   
}
