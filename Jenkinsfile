pipeline {
    agent any
    stages {
        stage('Maven Version') {
            steps {
                sh 'echo Print Maven Version'
                sh 'mvn -version'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests=true'
                archiveArtifacts 'target/hello-demo-*.jar'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                junit(testResults: 'target/surefire-reports/TST-*.xml', keepProperties: true, keepTestNames: true)
            }
        }
    }
}

