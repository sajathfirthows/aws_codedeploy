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

        stage('Build and Package') {
            steps {
                script {
                    // Use the Maven tool configured in Jenkins
                    def mavenHome = tool 'Maven'
                    sh "${mavenHome}/bin/mvn clean install"
                    
                    // Package your application (create a jar or war file)
                    sh 'cp target/saja-new-app.jar .'
                }
            }
        }

        stage('Upload to S3') {
            steps {
                script {
                    // Upload the application artifact to S3
                    sh 'aws s3 cp saja-new-app.jar s3://my-app-saja-cd/'
                }
            }
        }

        stage('Deploy to EC2') {
            steps {
                script {
                    // Trigger CodeDeploy deployment
                    sh 'aws deploy create-deployment --application-name saja-new-app --deployment-group-name saja-new-app-dg --s3-location bucket=my-app-saja-cd,key=saja-new-app.jar,bundleType=zip'
                }
            }
        }
    }

    post {
        always {
            echo "Post-deployment steps or cleanup can go here"
        }
    }
}
