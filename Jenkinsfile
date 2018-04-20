pipeline {
    agent any
	stages { 
		stage('SCM checkout') {
			steps {
			git url: 'https://github.com/shivendrapro0/jenkins-demo.git'
			}
		}
		stage('Build NodeApp') { 
		    steps {
		        sh 'npm install'
		        sh 'ng build'
		    }   
		}
		stage('Stop Docker Instance') { 
		    steps {
		        sh 'docker stop app1 || true'
		        sh 'docker rm app1 || true'
		    }   
		}
		stage('Re-build Image') { 
		    steps {
		        sh 'docker build . --tag nodeapp:v1'
		    }   
		}
		stage('Run Docker Instance') { 
		    steps {
		        sh 'docker run -d -p 8080:8080 --name app1 nodeapp:v1'
		    }   
		}
	}

}
