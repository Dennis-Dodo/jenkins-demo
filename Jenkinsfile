pipeline {
    agent any
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        jdk "JAVA_HOME"
    }
    stages {
        stage('Build') {
            steps {
                git 'https://github.com/Dennis-Dodo/jenkins-demo.git'
                bat './mvnw clean compile'
                // bat '.\mvnw clean compile'
            }
        }
        stage('Test') {
            steps {
                bat './mvnw test'
                // bat '.\mvnw test'
            }

            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Publish') {
            steps {
                bat './mvnw package'
                // bat '.\mvnw package'
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
