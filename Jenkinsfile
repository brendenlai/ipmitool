node {
	
	//def server = Artifactory.server SERVER_ID;
	//http://localhost:8081/artifactory
	def server = Artifactory.newServer url: 'http://localhost:8081/artifactory', username: 'admin', password: '1234'
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
		buildInfo1.env.capture = true      
		// Publish the build to Artifactory
		server.publishBuildInfo buildInfo1

	}
	
	stage('Approve') { 
		
		// 
		input "Does the staging environment look ok?"
		
	}
   
}
