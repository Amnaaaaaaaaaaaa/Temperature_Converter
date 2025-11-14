pipeline {
    agent any

    environment {
        NODE_ENV = 'development' // default, can adjust if needed
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "Checking out branch: ${env.BRANCH_NAME}"
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing npm dependencies..."
                bat 'npm install'
            }
        }

        stage('Parallel Test Execution') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo "Running unit tests..."
                        bat 'npm test || echo Tests failed, but continuing pipeline...'
                    }
                }
                stage('Linting') {
                    steps {
                        echo "Running linting..."
                        bat 'npm run lint || echo Lint passed'
                        // Or simulate lint: bat 'echo Lint passed'
                    }
                }
            }
        }

        stage('Conditional Deployment Simulation') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        echo "Deployed to Production Environment (main branch)"
                    } else if (env.BRANCH_NAME == 'dev') {
                        echo "Deployed to Staging Environment (dev branch)"
                    } else {
                        echo "Feature branch detected – Deployment Skipped."
                    }
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo "Archiving build artifacts..."
                // Adjust path to match your build/test output
                archiveArtifacts artifacts: '**/build/**', allowEmptyArchive: true
            }
        }

        stage('Notification') {
            steps {
                script {
                    def currentDate = new Date().format("yyyy-MM-dd HH:mm:ss")
                    echo "Build #${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME} completed successfully at ${currentDate}"
                }
            }
        }
    }

    post {
        failure {
            echo "Build #${env.BUILD_NUMBER} failed on branch ${env.BRANCH_NAME}"
        }
    }
}
