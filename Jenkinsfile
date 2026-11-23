pipeline {
    agent any

    environment {
        IMAGE_NAME = "devops-portfolio-app"
    }

    stages {
        stage('Install') {
            steps {
                sh 'python3 -m venv .venv'
                sh '. .venv/bin/activate && pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh '. .venv/bin/activate && pytest'
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} ."
            }
        }
    }

    post {
        always {
            echo "Build ${BUILD_NUMBER} finished"
        }
    }
}
