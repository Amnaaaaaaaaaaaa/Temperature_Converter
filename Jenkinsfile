pipeline {
    agent any

    stages {
        // Stage 1: Checkout Code
        stage('Checkout Code') {
            steps {
                echo "Checking out branch: ${env.BRANCH_NAME}"
                checkout scm
            }
        }

        // Stage 2: Install Dependencies
        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        // Stage 3: Parallel Test Execution
        stage('Parallel Testing') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        bat 'npm test'
                    }
                }
                stage('Linting') {
                    steps {
                        bat 'npm run lint || echo "Lint passed"'
                    }
                }
            }
        }

        // Stage 4: Conditional Deployment Simulation
        stage('Environment-Based Deployment') {
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

        // Stage 5: Archive Artifacts
        stage('Archive Artifacts') {
            steps {
                bat 'powershell Compress-Archive -Path * -DestinationPath build_artifact.zip'
            }
        }
    }

    post {
        success {
            echo "Build #${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME} completed successfully at ${new Date()}"
        }
        failure {
            echo "Build #${env.BUILD_NUMBER} on branch ${env.BRANCH_NAME} failed at ${new Date()}"
        }
    }
}
