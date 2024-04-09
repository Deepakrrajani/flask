pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'pip install -r flask'
            }
        }
        stage('Test') {
            steps {
                sh 'pytest'
            }
        }
        stage('Deploy') {
            steps {
                // In a real-world scenario, you would deploy to your server here
                sh 'echo "Deployment step"'
            }
        }
    }

    post {
        always {
            // Clean up steps can be added here
        }
        success {
            echo 'Pipeline succeeded! Deploying...'
        }
        failure {
            echo 'Pipeline failed! Please check the build logs.'
        }
    }
}
