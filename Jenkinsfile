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
            
            // Specify the directory where the Maven project is located
            def mavenProjectDir = 'path/to/your/maven/project'
            
            // Execute Maven in the specified directory
            sh "cd ${mavenProjectDir} && ${mavenHome}/bin/mvn clean install"
            
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
