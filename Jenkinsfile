pipeline {
  environment {
    registry = "ybmsr/docker-java-42"
    registryCredential = 'dockerhub_credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('get scm') {
      steps {
	  git branch: 'main', credentialsId: 'github_new_credentials', url: 'https://github.com/jmstechhome25/hello-world-docker.git'
       }
    }

    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":v$BUILD_NUMBER"
        }
      }
    }
    stage('push image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove old docker image') {
      steps{
        sh "docker rmi $registry:v$BUILD_NUMBER"
      }
    }
  }
}
