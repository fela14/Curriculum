pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds') // your Jenkins credentials ID
    }
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
                        sh 'echo Hello from Linux'
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
            steps {
                // DOCKERHUB_CREDENTIALS_USR and DOCKERHUB_CREDENTIALS_PSW
                sh 'docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW'
            }
        }

        stage('Push') {
            steps {
                sh 'docker push fela14/curriculum-front:latest'
            }
        }
    }
}
