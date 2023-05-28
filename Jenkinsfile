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
	stages {
		stage ('Build')
		  steps { 
			echo "Build"
		  }
	stage ('Test') {
		steps {
           echo "Test"
		}
	}
	stage ('Integration Test') {
		steps {
           echo "Integration Test"
		}
	}
	}
}
