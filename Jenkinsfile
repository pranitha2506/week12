pipeline {
    agent any
    stages
    {
        
stage('Run Selenium Tests with pytest') {
    steps {
        echo "Running Selenium Tests using pytest"

        bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" --version'

        bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m pip install -r requirements.txt'

        bat 'start /B "" "C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" app.py'

        bat 'ping 127.0.0.1 -n 5 > nul'

        bat '"C:\\Users\\DELL\\AppData\\Local\\Programs\\Python\\Python313\\python.exe" -m pytest -v'
    }
}

        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u pranithapadtham -p Pranitha@123'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag kubdemoapp:v1 pranithapadtham/week8:kubeimage1"               
                    
                bat "docker push pranithapadtham/week8:kubeimage1"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                    // apply deployment & service 
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
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
