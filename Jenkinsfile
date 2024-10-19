pipeline {
    agent any
        environment {
        MAVEN_VERSION = '3.8.6'
        MAVEN_HOME = "${WORKSPACE}/maven"
    }

    stages {
        stage('Install Maven') {
            steps {
                script {
                    if (!fileExists("${MAVEN_HOME}/bin/mvn")) {
                        bat """
                        echo Downloading Maven ${MAVEN_VERSION}
                        wget https://downloads.apache.org/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.zip

                        echo Extracting Maven
                        PowerShell -Command "Expand-Archive -Path 'apache-maven-${MAVEN_VERSION}-bin.zip' -DestinationPath '.'"

                        echo Moving Maven folder
                        move apache-maven-${MAVEN_VERSION} maven
                        """
                    }
                }
            }
        }

        stage('Build') {
            steps {
                bat "${MAVEN_HOME}/bin/mvn clean install"
            }
        }





        stage('Test') {
            steps {
                // Run unit tests
                bat 'mvn test'
            }
        }

        stage('Package') {
            steps {
                // Package the application
                bat 'mvn package'
            }
        }
        
        stage('Docker Build') {
            steps {
                script {
                    // Build the Docker image
                    bat 'docker build -t myapp:latest .'
                }
            }
        }
        
        stage('Docker Push') {
            steps {
                script {
                    // Push Docker image to Docker Hub
                    withCredentials([string(credentialsId: 'dockerhub-credentials', variable: 'DOCKER_HUB_PASSWORD')]) {
                        bat 'docker login -u rajkumarjayampu -p Rajkumar@113'
                        bat 'docker tag myapp:latest rajkumarjayampu/myapp:latest'
                        bat 'docker push rajkumarjayampu/myapp:latest'
                    }
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deploy the Docker container
                    bat 'docker run -d -p 8080:8080 rajkumarjayampu/myapp:latest'
                }
            }
        }
    }
}

