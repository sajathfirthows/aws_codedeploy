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
                    // Change to the directory where the Maven project is located
                    dir('path/to/your/maven/project') {
                        // Use the Maven tool configured in Jenkins
                        def mavenHome = tool 'Maven'
                        sh "${mavenHome}/bin/mvn clean install"
                        
                        // Package your application (create a jar or war file)
                        sh 'cp target/saja-new-app.jar .'
                    }
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
