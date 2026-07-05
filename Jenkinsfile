pipeline {
  agent any
  environment {
    DOCKER_CRED = credentials('Docker')
  }
  stages {
    stage('fetch-code') {
      steps {
        git branch: 'main', url: 'https://github.com/divyasai-svg/assign4.git'
      }
    }
    stage('build-image') {
      steps {
        sh 'docker build -t divyamull/add4:${BUILD_NUMBER} .'
      }
    }
    stage('push-image') {
      steps {
        sh ' echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
        sh 'docker push divyamull/add4:${BUILD_NUMBER}'
      }
    }
    stage('update-minikube') {
      steps {
        sh 'kubectl set image deployment/dd4 add4=divyamull/add4:${BUILD_NUMBER}'
      }
    }
  }
}
