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
            bat 'echo Hello from Windows Batch'
          }
        }

        stage('Front-End Unit Tests') {
          steps {
            bat 'cd curriculum-front && npm i && npm run test:unit'
          }
        }

      }
    }

    stage('Build') {
      steps {
        bat 'docker build -f curriculum-front/Dockerfile .'
      }
    }

  }
}