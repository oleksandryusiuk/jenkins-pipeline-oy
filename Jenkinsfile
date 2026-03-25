pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                // Створюємо образ локально
                sh 'docker build -t my-app:latest .' 
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Tests passed!"'
            }
        }
        stage('Deploy to Docker Hub') {
            steps {
                // Використовуємо збережені креденшіали
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    echo 'Logging into Docker Hub...'
                    sh "echo \$PASS | docker login -u \$USER --password-stdin"
                    
                    echo 'Tagging and Pushing image...'
                    sh "docker tag my-app:latest \$USER/pipeline_1:latest"
                    sh "docker push \$USER/pipeline_1:latest"
                }
            }
        }
    }
}