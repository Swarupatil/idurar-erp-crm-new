pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/Swarupatil/idurar-erp-crm-new.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t mern-backend .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t mern-frontend .'
                }
            }
        }

        stage('Deploy Containers') {
            steps {
                sh '''
                docker rm -f backend frontend || true
                docker run -d --name backend -p 5000:5000 mern-backend
                docker run -d --name frontend -p 3000:80 mern-frontend
                '''
            }
        }
    }
}
