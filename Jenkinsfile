pipeline {

  stages {
    stage('Clone repository') {

          checkout scm
    }

    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build mysite
        }
      }
    }
    stage('Push image') {
                                                  docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
       app.push("${env.BUILD_NUMBER}")
       app.push("latest")
    }

  }
}
