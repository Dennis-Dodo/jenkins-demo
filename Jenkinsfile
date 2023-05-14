pipeline {
    agent any
    tools {
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
                stage('Unit Test') {
                    steps {
                        sh './mvnw test'
                    }
                }
                stage('Integration Test') {
                    steps {
                        sh './mvnw verify -DskipUnitTests -Parq-wildfly-swarm'
                    }
                }
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
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
