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
                bat 'javac Factorial.java'  // Use bat instead of sh
            }
        }

        stage('Test') {
            steps {
                script {
                    // Use bat for Windows
                    def output = bat(script: 'java Factorial', returnStdout: true).trim()
                    echo output
                }
            }
        }

        stage('Package as WAR') {
            steps {
                bat '''  // Use bat and Windows commands
                    mkdir webapp\\WEB-INF\\classes
                    copy Factorial.class webapp\\WEB-INF\\classes\\
                    jar cvf factorial.war -C webapp .
                '''
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''  // Use bat for Windows
                    curl --upload-file factorial.war "http://localhost:8080/manager/text/deploy?path=/factorial&update=true" --user admin:admin
                '''
            }
        }
    }

    post { 
        // ... (keep post section as-is)
    }
}
