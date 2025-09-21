pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:PradnyaAvhad21/cicd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build --no-cache -t cicd-demo-app .'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def containerExists = sh(script: "docker ps -a -q -f name=cicd-demo-app", returnStdout: true).trim()
                    if (containerExists) {
                        sh "docker rm -f cicd-demo-app"
                    }
                    sh "docker run -d -p 5000:5000 --name cicd-demo-app cicd-demo-app"
                }
            }
        }
    }
}
