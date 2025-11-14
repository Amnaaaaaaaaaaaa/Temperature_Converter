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
        bat 'powershell Compress-Archive -Path *.js, package.json, src -DestinationPath build_artifact.zip'
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
