pipeline {
    agent any 
    stages {
        stage('clone from repo') { 
            steps {
                // 
                sh "echo clone from repo"
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
            }
        }
    }
}
