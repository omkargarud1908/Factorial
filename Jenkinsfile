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
                script {
                    if (isUnix()) {
                        sh 'mvn clean package'
                    } else {
                        bat 'mvn clean package'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn test'
                    } else {
                        bat 'mvn test'
                    }
                }
            }
        }

        stage('Package as WAR') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'mvn package'
                    } else {
                        bat 'mvn package'
                    }
                }
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    def tomcatPath = 'C:\\Tomcat' // Change this path accordingly
                    if (isUnix()) {
                        sh 'cp target/*.war /path/to/tomcat/webapps/'
                    } else {
                        bat "copy target\\*.war ${tomcatPath}\\webapps\\"
                    }
                }
            }
        }
    }

    post {
        failure {
            emailext subject: 'Build Failed',
                    body: 'The build has failed. Please check Jenkins logs.',
                    to: 'omkargarud495@gmail.com'
        }
    }
}
