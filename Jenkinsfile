pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from SCM
                checkout scm
            }
        }
        stage('Print Maven Version') {
            steps {
                sh 'mvn -version'
            }
        }
        stage('Build') {
            steps {
                // Build the project, skip tests to speed it up
                sh 'mvn clean package -DskipTests'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                junit 'target/surefire-reports/TEST-*.xml'
            }
        }
    }

    post {
        always {
            cleanWs()  // Clean workspace regardless of build result
        }
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
