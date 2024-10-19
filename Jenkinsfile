pipeline {
    agent any
    
    stages {
        stage('Checkout Code') {
            steps {
                // Clone the repository from Git
                git url: 'https://github.com/Rajkumarjayampu/sampletest.git', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                // Compile the project using Maven
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run unit tests
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the application
                sh 'mvn package'
            }
        }
        
        stage('Docker Build') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t myapp:latest .'
                }
            }
        }
        
        stage('Docker Push') {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    withCredentials([string(credentialsId: 'dockerhub-credentials', variable: 'DOCKER_HUB_PASSWORD')]) {
                        sh 'docker login -u rajkumarjayampu -p Rajkumar@113'
                        sh 'docker tag myapp:latest rajkumarjayampu/myapp:latest'
                        sh 'docker push rajkumarjayampu/myapp:latest'
                    }
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy the Docker container
                    sh 'docker run -d -p 8080:8080 rajkumarjayampu/myapp:latest'
                }
            }
        }
    }
}

