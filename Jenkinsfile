pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/omkargarud1908/Factorial.git'
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

        stage('Package as WAR') {
            steps {
                sh '''
                mkdir -p webapp/WEB-INF/classes
                cp Factorial.class webapp/WEB-INF/classes/
                jar cvf factorial.war -C webapp .
                '''
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                curl --upload-file factorial.war "http://localhost:8080/manager/text/deploy?path=/factorial&update=true" \
                --user admin:admin
                '''
            }
        }
    }

    post {
        success {
            emailext(
                to: 'omkargarud8833@gmail.com',
                subject: 'Jenkins Build Success',
                body: 'The factorial application has been successfully built and deployed to Tomcat.'
            )
        }
        failure {
            emailext(
                to: 'omkargarud8833@gmail.com',
                subject: 'Jenkins Build Failed',
                body: 'The build or deployment process failed. Please check the logs.'
            )
        }
    }
}
