pipeline {
    agent any

  stage('Run Selenium Tests with pytest') {
            steps {
                echo "Running Selenium Tests using pytest"

                // Install Python dependencies
                bat 'python -m pip install -r requirements.txt'

                // Start Flask application in background
                bat 'start /B python app.py'

                // Wait for Flask application to start
                bat 'ping 127.0.0.1 -n 5 > nul'

                // Run Selenium tests
                bat 'python -m pytest -v'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Build Docker Image'
                bat 'docker build --no-cache -t kubdemoapp:v1 .'
            }
        }

        stage('Docker Login') {
            steps {
                bat 'docker login -u pranithapadtham -p Pranitha@123'
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                echo 'Push Docker Image to Docker Hub'
                bat 'docker tag kubdemoapp:v1 pranithapadtham/week8:image1'
                bat 'docker push pranithapadtham/week8:image1'
            }
        }

       
 stage('Deploy to Kubernetes') {
    steps {
        bat 'set KUBECONFIG=C:\\ProgramData\\Jenkins\\.kube\\config && kubectl apply -f deployment.yaml --validate=false'
        bat 'set KUBECONFIG=C:\\ProgramData\\Jenkins\\.kube\\config && kubectl apply -f service.yaml'
    }
}
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
