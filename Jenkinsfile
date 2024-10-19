pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from SCM (Git)
                git url: 'https://github.com/Rajkumarjayampu/sampletest.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Running a basic Windows batch command
                bat 'echo Building the project...'
                bat 'echo Build complete.'
            }
        }

        stage('Test') {
            steps {
                // Running tests via batch commands
                bat 'echo Running tests...'
                bat 'echo All tests passed.'
            }
        }

        stage('Package') {
            steps {
                // Simulate packaging
                bat 'echo Packaging the build...'
                bat 'echo Package complete.'
            }
        }

        stage('Archive') {
            steps {
                // Archive build artifacts (dummy file in this case)
                bat 'echo Creating artifact...'
                bat 'echo Hello World > output.txt'
                archiveArtifacts artifacts: 'output.txt', allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            // Clean up workspace after build
            cleanWs()
        }
    }
}

