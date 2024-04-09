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
                // Create deployment directory if it doesn't exist
                sh 'ssh ec2-user@3.83.3.224 "mkdir -p /home/ec2-user/flask_app"'
                // Deploy the Flask application files to the deployment directory
                sh 'scp main.py ec2-user@3.83.3.224:/home/ec2-user/flask_app'
                // You may need to copy other necessary files as well
                // Start the Flask application
                sh 'ssh ec2-user@3.83.3.224 "cd /home/ec2-user/flask_app && python main.py &"'
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
