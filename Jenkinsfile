pipeline {
    agent any

    environment {
        APPLICATION_NAME = 'saja-new-app'
        DEPLOYMENT_GROUP_NAME = 'saja-new-dg'
        GITHUB_REPO = 'https://github.com/sajathfirthows/aws_codedeploy'
        GITHUB_COMMIT = 'master'  // Replace with the specific branch or commit ID
        GRADLE_HOME = tool 'Gradle' // Assuming you have Gradle configured in Jenkins as a tool
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/sajathfirthows/aws_codedeploy']]])
                }
            }
        }

        stage('Build with Gradle') {
            steps {
                script {
                    withEnv(['PATH+GRADLE=${env.GRADLE_HOME}/bin']) {
                        sh './gradlew build'
                    }
                }
            }
        }

        stage('Deploy to CodeDeploy') {
            steps {
                script {
                    sh "aws deploy create-deployment --application-name $APPLICATION_NAME --deployment-group-name $DEPLOYMENT_GROUP_NAME --github-location repository=$GITHUB_REPO,commitId=$GITHUB_COMMIT"
                }
            }
        }
    }

    post {
        always {
            script {
                // Assuming you have the necessary plugins for GitHub integration
                // Update this section based on your actual requirements
                githubStatus context: 'continuous-integration/jenkins', state: 'success'
                if (env.CHANGE_ID) {
                    githubComment message: "The pipeline completed successfully!"
                    githubLabel labels: ['approved']
                }
            }
        }
    }
}
