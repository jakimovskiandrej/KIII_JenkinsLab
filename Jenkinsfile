pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        script {
          sh "docker build -t ${DOCKER_USER}/kiii-lab:latest ."
        }

      }
    }

    stage('Push image') {
      steps {
        script {
          sh "echo \$DOCKER_HUB_CREDS_PSW | docker login -u \$DOCKER_HUB_CREDS_USR --password-stdin"
          sh "docker push ${DOCKER_USER}/kiii-lab:latest"
        }

      }
    }

  }
  environment {
    DOCKER_USER = 'jakimovskiandrej'
  }
  post {
    success {
      echo 'Апликацијата е успешно изградена и пратена на Docker Hub!'
    }

    failure {
      echo 'Процесот не успеа. Провери ги лозинките или лог фајловите.'
    }

  }
}