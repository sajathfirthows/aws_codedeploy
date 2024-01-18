pipeline {
    agent any

    tools {
        // Configure Git tool
        git 'GIT_TOOL_NAME'
        // Configure Gradle tool (if applicable)
        gradle 'GRADLE_TOOL_NAME'
    }

    options {
        skipDefaultCheckout true
    }

    environment {
        REPO_URL = 'https://github.com/sajathfirthows/aws_codedeploy.git'
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Ensure Git is properly configured in the workspace
                    checkout([$class: 'GitSCM', branches: [[name: env.BRANCH_NAME]], userRemoteConfigs: [[url: env.REPO_URL]]])
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Assuming you have Gradle configured in Jenkins as a tool
                    withEnv(['PATH+GRADLE=${tool 'GRADLE_TOOL_NAME'}/bin']) {
                        sh './gradlew build'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    withEnv(['PATH+GRADLE=${tool 'GRADLE_TOOL_NAME'}/bin']) {
                        sh './gradlew test'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh './deploy.sh'
                }
            }
        }
    }

    post {
        always {
            script {
                // Assuming you have the necessary plugins for GitHub integration
                // Update this section based on your actual requirements
                script {
                    // Assuming you have the necessary plugins for GitHub integration
                    // Update this section based on your actual requirements
                    script {
                        try {
                            // If you have the GitHub plugin installed, update the status
                            githubStatus context: 'continuous-integration/jenkins', state: 'success'
                            if (env.CHANGE_ID) {
                                githubComment message: "The pipeline completed successfully!"
                                githubLabel labels: ['approved']
                            }
                        } catch (Exception e) {
                            echo "Failed to update GitHub status: ${e.message}"
                        }
                    }
                }
            }
        }
    }
}
