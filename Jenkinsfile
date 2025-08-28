pipeline {
  agent any
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/fela14/Curriculum.git', branch: 'main')
      }
    }

    stage('Tests') {
      parallel {
        stage('Tests') {
          steps {
            sh 'echo Hello from Windows Batch'
          }
        }

        stage('Front-End Unit Tests') {
          steps {
            sh 'cd curriculum-front && npm i && npm run test:unit'
          }
        }

      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile . -t fela14/curriculum-front:latest'
      }
    }

    stage('Log into Dockerhub') {
      environment {
        DOCKERHUB_USERNAME = 'fela14'
        DOCKERHUB_PASSWORD = 'Oluwaseun_60'
      }
      steps {
        sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push fela14/curriculum-front:latest'
      }
    }

  }
}