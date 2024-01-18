pipeline {
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

        stage('Build') {
            steps {
                script {
                    // Your build steps here (e.g., Maven build for Java)
                    def mavenHome = tool 'Maven'
                    sh "${mavenHome}/bin/mvn clean install"
                }
            }
        }

        stage('Deploy to AWS CodeDeploy') {
            steps {
                script {
                    // Trigger AWS CodeDeploy deployment
                    sh 'aws deploy create-deployment --application-name saja-new-app --deployment-group-name saja-new-app-dg --s3-location bucket=my-app-saja-cd,key=saja-new-app.jar,bundleType=zip'
                }
            }
        }
    }

    post {
        always {
            // Cleanup or post-deployment steps
        }
    }
}
