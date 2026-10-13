
pipeline {
    agent any

    stages {
       stage("Run Selenium Tests with pytest") {
    steps {
        echo "Checking Python environment"

        bat 'where python'
        bat 'python --version'
        bat 'python -m pip --version'
        bat 'python -m pip list'

        bat 'python -m pip install -r requirements.txt'
        bat 'start /B python app.py'
        bat 'ping 127.0.0.1 -n 5 > nul'
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
}
