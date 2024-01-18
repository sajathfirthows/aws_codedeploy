pipeline {
    agent any

    tools {
        // Specify the Gradle installation configured in Jenkins
        gradle 'Gradle'
    }

    stages {pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout source code from GitHub
                    git 'https://github.com/sajathfirthows/aws_codedeploy'
                }
            }
        }

        stage('Build and Package') {
            steps {
                script {
                    // Use the Gradle tool configured in Jenkins
                    def gradleHome = tool 'Gradle'
                    
                    // Specify the relative path to your Gradle project
                    def gradleProjectDir = '/var/lib/jenkins/tools/hudson.plugins.gradle.GradleInstallation/Gradle'

                    // Execute Gradle in the specified directory
                    sh "cd ${gradleProjectDir} && ${gradleHome}/bin/gradle clean build"

                    // Upload the artifact to S3
                    sh 'aws s3 cp build/libs/saja-new-app.jar s3://my-app-saja-cd/'

                    // Optionally, you can copy the artifact to the workspace for later stages
                    sh 'cp build/libs/saja-new-app.jar .'
                }
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

        // ... your stages
    }

    post {
        always {
            echo "Post-deployment steps or cleanup can go here"
        }
    }
}
