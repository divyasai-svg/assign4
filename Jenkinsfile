pipeline {
  agent any
  environment {
    DOCKER_CRED = credentials('DockerHub')
  }
  stages {
    stage('fetch-code') {
      steps {
        git branch: 'main', url: 'https://github.com/divyasai-svg/asn4.git'
      }
    }
    stage('build-image') {
      steps {
        sh 'docker build -t divyamull/ad4:${BUILD_NUMBER} .'
      }
    }
    stage('push-image') {
      steps {
        sh ' echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
        sh 'docker push divyamull/ad4:${BUILD_NUMBER}'
      }
    }
    stage('update-minikube') {
      steps {
        sh 'kubectl set image deployment/d4 ad4=divyamull/ad4:${BUILD_NUMBER}'
      }
    }
  }
}
