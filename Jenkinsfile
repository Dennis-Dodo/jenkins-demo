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
                sh './mvnw clean compile'
                sh './mvnw clean install -DskipTests'
            }
        }
        stage('Test') {
            steps {
                sh './mvnw test'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Integration Test') {
            steps {
                sh 'mvn verify -DskipUnitTests -Parq-wildfly-swarm '
            }
        }
        stage('Publish') {
            steps {
                sh './mvnw package'
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
