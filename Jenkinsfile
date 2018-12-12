node {
	
	def server = Artifactory.server SERVER_ID;
	def uploadSpec 
	def buildInfo1
  //  agent any 
    
    stage('Clone'){ 
		
		// 
		git url: 'https://github.com/brendenlai/ipmitool.git'
		
	}
        
	stage('Build') { 
		
		// 
		sh "echo building .... "
		sh "./configure"
		sh "autoreconf -ivf"
		sh "make"
		
	}
	stage('Deploy') { 
		
		// 
		sh "echo Deploying .... "
		

		// Read the upload spec which was downloaded from github.
		uploadSpec = readFile 'resource/ipmitool-upload.json'
		// Upload to Artifactory.
		buildInfo1 = server.upload spec: uploadSpec       
		// Publish the build to Artifactory
		server.publishBuildInfo buildInfo1

	}
   
}
