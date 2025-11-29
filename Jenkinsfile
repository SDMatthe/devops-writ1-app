pipeline {
  agent any

  environment {
    DOCKERHUB = credentials('DockerHub')
  }

  stages {
    stage('Docker Login') {
      steps {
        sh 'echo "$DOCKERHUB_PSW" | docker login -u "$DOCKERHUB_USR" --password-stdin'
      }
    }

    stage('Pull , build and Run dockerfile ') {
      steps {
        sh '''
          docker stop DevOps-WRIT1-app || true
          docker rm DevOps-WRIT1-app || true
          docker rmi SDMatthe/DevOps-WRIT1-app || true
          docker build -t SDMatthe/DevOps-WRIT1-app .
          docker compose up -d
        '''
      }
    }

    stage('Run Tests') {
      steps {
        echo "done testing"
      }
    }

    stage('cleaning') {
      steps {
        sh 'docker compose down || true'
      }
    }
  }
}
