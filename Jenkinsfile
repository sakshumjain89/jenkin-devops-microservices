pipeline {
	agent any
	//agent { docker {image 'maven:3.6.3' }}
	//agent { docker {image 'node:13.8' }}
	environment {
		dockerHome = tool 'mydocker'
        mavenHome = tool 'mymaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage ("Check Out") {
			steps {
				sh 'mvn --version'
				sh 'docker version'
				echo "Check Out"
				echo "PATH - $PATH"
				echo "BUILD NUMBER - $env.BUILD_NUMBER"
				echo "Build ID - $env.BUILD_ID"
				echo "JOB NAME - $env.JOB_NAME"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "BUILD_URL - $env.BUILD_URL"
			}
		}
		stage ("Compile") {
			steps {
				sh "mvn clean compile"
			}
		}
		stage ("Test") {
			steps {
				sh "mvn test"
			}
		}
		stage ("Integration Test") {
			steps {
				sh "mvn failsafe:integration-test failsafe:verify"
			}
		}
	} 
	
	post {
		always {
			echo "I'm Awesome! I run always"
		}
		success {
			echo "I run when you are successful"
		}
		failure {
			echo "I run when you fail"
		}
	}
}
