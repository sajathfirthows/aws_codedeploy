pipeline {
    agent any

    tools {
        // Specify the Gradle installation configured in Jenkins
        gradle 'YourGradleInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sajathfirthows/aws_codedeploy'
            }
        }

        stage('Build and Package') {
            steps {
                // Gradle will be available in the PATH with GRADLE_HOME set
                sh 'gradle clean build'

                // ... rest of the script
            }
        }

        // ... other stages

    }

    post {
        always {
            echo "Post-deployment steps or cleanup can go here"
        }
    }
}
