pipeline {
    agent any
    tools {
        maven "maven3.8.3"
        jdk "jdk-17.0.1"
    }
    stages {
        stage("Env Variables") {
            steps {
                bat "printenv"
            }
        }
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Site') {
            steps {
                bat 'mvn site'
            }
        }
    }
}