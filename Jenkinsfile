// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('integeration Test') {
// 		echo "Test"
// 	}
// }
//scripted
// node {
// {
// 		echo "Build"
// 	
// 		echo "Test"
// 	
// 		echo "Test"
// 	}
// }

//Declarative

pipeline {
	agent any
	//agent {docker {image 'maven:3.6.3'}}
	//agent {docker {image 'node:13.8'}}  //using docker image and run it their
	environment {
		dockerHome = tool 'myDocker'
		mavenHome = tool 'myMaven'
		PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
	}
	stages {
		stage ('checkout'){
		  steps { 
			 sh 'mvn --version'
			 sh 'docker version'
			 echo "Build"
			 echo "PATH - $PATH"
			 echo "BUILD_NUMBER - $env.BUILD_NUMBER"
			 echo "BUILD_ID - $env.BUILD_ID"
			 echo "JOB_NAME - $env.JOB_NAME"
			 echo "BUILD_TAG - $env.BUILD_TAG"
			 echo "BUILD_URL - $env.BUILD_URL"
		  }
		}
	    stage ('Compile') {
		  steps {
             sh "mvn clean compile"
		}
	}
	    stage ('Test') {
		  steps {
             echo "mvn Test"
		}
	}
	    stage ('Integration Test') {
		  steps {
             echo "mvn failsafe integration-Test failsafe:verify"
		}
	}
	    stage ('package') {
		  steps {
			sh "mvn package -DskipTests"
             echo "mvn failsafe integration-Test failsafe:verify"
		}	
	    stage ('Build Docker Image'){
			steps {
				//"docker build -t shubhamad/currency-exchange-devops:$env.BUILD_TAG"
				script {
					dockerImage=docker.build("shubhamad/currency-exchange-devops:${env.BUILD_TAG}")
				}
			}
		}
	    stage ('Push Docker Image'){
			steps {
				docker.withRegistry('',dockerhub){
				dockerImage.push();
				dockerImage.push('latest');
				}
			}
		}
	}
	post {
		always {
			echo 'Im awesome. I run always'
		}
		success {
			echo 'I run when you are successful'
		}
		failure {
			echo 'I run when you are failed'
		}
		
	}
}
