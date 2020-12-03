pipeline {
	environment {
		registry = 'vicky4u012/myproject1'
		registryCredential = 'dockerId'
		dockerImage = ''
	}
	agent any
	tools {nodejs 'node1'}
	stages {
		stage('cloning Git'){
			steps{
				git 'https://github.com/vicky4u012/DockerizeJenkins.git'
			}
		}
		stage('Build'){
			steps {
				sh 'npm install'
				sh 'npm run bowerInstall'
			}
		}
		stage('Test'){
			steps {
				sh 'npm test'
			}
		}
		stage('Building image'){
			steps{
				script {
					dockerImage = docker.build registry + "$BUILD_NUMBER"
				}
			}
		}
		stage('Deploy Image'){
			steps{
				script {
					docker.withRegistry( '', registryCredential ){
					dockerImage.push()
					}
				}
			}
		}
	}
}
