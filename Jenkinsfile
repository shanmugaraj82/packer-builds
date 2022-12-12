pipeline {
  agent any
  stages {
    stage('Cloning our Git') {
      steps {
        git 'https://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@github.com/shanmugaraj82/packer-builds.git'
      }
    }

    stage('Building our image') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }

      }
    }

    stage('Deploy our image') {
      steps {
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }

      }
    }

    stage('Cleaning up') {
      steps {
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }

  }
  environment {
    registry = 'YourDockerhubAccount/YourRepository'
    registryCredential = 'dockerhub_id'
    dockerImage = ''
  }
}
