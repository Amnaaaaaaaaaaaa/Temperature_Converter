pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Amnaaaaaaaaaaaa/Temperature_Converter.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Lint') {
            steps {
                bat 'npm run lint || echo "Linting failed!"'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Archive Build Artifact') {
            steps {
                // Create a zip file (Windows)
                bat 'powershell Compress-Archive -Path * -DestinationPath build_artifact.zip'
                
                // Publish the artifact
                archiveArtifacts artifacts: 'build_artifact.zip', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "Build Success! Email sent to team@example.com"
        }
        failure {
            echo "Build Failed! Email sent to team@example.com"
        }
    }
}
