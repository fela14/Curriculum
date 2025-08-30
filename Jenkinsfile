pipeline {
    agent { label 'linux-agent' } // runs all stages on your Linux agent
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhb') // your Jenkins credentials ID
    }
    stages {
        stage('Checkout Code') {
            steps {
                git(url: 'https://github.com/fela14/Curriculum.git', branch: 'main')
            }
        }

        stage('Debug Front-End') {
            steps {
                dir('curriculum-front') {
                    sh 'ls -R src/components'
                }
            }
        }

        stage('Tests') {
            steps {
                sh 'echo Hello from Linux'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -f curriculum-front/Dockerfile . -t fela14/curriculum-front:latest'
            }
        }

        stage('Log into Dockerhub') {
            steps {
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
