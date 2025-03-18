pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/omkargarud1908/Factorial.git' 
            }
        }

        stage('Build') {
            steps {
                sh 'javac Factorial.java'
            }
        }

        stage('Test') {
            steps {
                script {
                    def output = sh(script: 'java Factorial', returnStdout: true).trim()
                    echo output
                }
            }
        }

        stage('Package') {
            steps {
                sh 'jar cf factorial.jar Factorial.class'
            }
        }

        stage('Deploy') {
            steps {
                sh 'scp factorial.jar user@yourserver:/opt/deploy/'
            }
        }
    }

    post {
        success {
            mail to: 'omkargarud8833@example.com',
                 subject: 'Jenkins Build Success',
                 body: 'The build and deployment of the factorial application were successful.'
        }
        failure {
            mail to: 'omkargarud8833@example.com',
                 subject: 'Jenkins Build Failed',
                 body: 'The build or deployment process failed. Please check the logs.'
        }
    }
}
