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
                stage('Build Container') {
	            when {
       		         branch 'integration'
                    }
                    steps {
                        sh 'docker build . --tag nodeapp-int'
                    }
                }
		stage('Run Container') { 
                    when {
                         branch 'master'
                    }
		    steps {
			sh 'docker build . --tag nodeapp-master'
                        sh 'docker stop app1 || true'
                        sh 'docker rm app1 || true'
		        sh 'docker run -d -p 8080:8080 --name app1 nodeapp-master' 
		    }   
		}
	}

}
