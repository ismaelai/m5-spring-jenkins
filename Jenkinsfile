pipeline {
    agent any
    tools {
        maven "maven.3.8.3"
        jdk "jdk-17.0.1"
    }
    stages {

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

        stage('Sonar'){
                    steps {
                      bat 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=m5-spring-jenkins-ismael -Dsonar.login=f8a6408e127d719e6b621535560b3e50e1e5375f -Dsonar.host.url=https://sonarcloud.io -Dsonar.organization=ismaelai'

                    }
                }

    }
}