pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/NoreenMazhar/flask-app-task.git' // Replace with your actual repository URL
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv venv
                source venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh '''
                source venv/bin/activate
                pytest tests/ --junitxml=test-report.xml
                '''
            }
        }

        stage('Build Application') {
            steps {
                sh '''
                echo "Preparing Flask application for deployment"
                # Optionally include packaging steps, e.g., Docker build
                '''
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                mkdir -p /var/www/FlaskApp
                cp -r . /var/www/FlaskApp
                echo "Flask application deployed to /var/www/FlaskApp"
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/test-report.xml', allowEmptyArchive: true
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}

