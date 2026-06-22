pipeline {
    agent any

    environment {
        VENV = "venv"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/flask-jenkins-ci-cd.git'
            }
        }

        stage('Setup Environment') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    . venv/bin/activate
                    pytest test_app.py
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Deploying Flask app..."
                    nohup python app.py > output.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            mail to: 'your-email@example.com',
                 subject: "SUCCESS: Jenkins Build Passed",
                 body: "Your Flask CI/CD pipeline executed successfully."
        }

        failure {
            mail to: 'your-email@example.com',
                 subject: "FAILED: Jenkins Build Failed",
                 body: "Check Jenkins logs for details."
        }
    }
}
