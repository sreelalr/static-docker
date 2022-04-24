pipeline {
  agent{
    node { label 'slavefordocker'}
  }
  environment {
    DOCKERHUB_CREDENTIALS= credentials('dockerhub')
  }
  stages {
    stage("Git Checkout"){
      checkout scm
    }
    stage('Build Docker Image') {
      steps{
	sh 'sudo docker build -t sreelalrp/mysite:$BUILD_NUMBER .'
        echo 'Build Image Completed'
      }
    }
    stage('Login to Docker Hub') {
      steps{
	sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
	echo 'Login Completed'
      }
    }
    stage('Push Image to Docker Hub') {
      steps{
	sh 'sudo docker push sreelalrp/mysite:$BUILD_NUMBER'                 echo 'Push Image Completed'       
      }
    }
  } //stages
  post{
    always {
      sh 'docker logout'
    }
  }
} //pipeline
