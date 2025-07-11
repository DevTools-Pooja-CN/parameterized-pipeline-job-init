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
                // Build the package, skipping tests to speed up
                sh 'mvn clean package -DskipTests=true'
                // Archive the built jar artifact
                archiveArtifacts 'target/hello-demo-*.jar'
            }
        }
        stage('Test') {
            steps {
                // Run tests separately
                sh 'mvn test'
                // Publish test results (check if TEST-*.xml matches your setup)
                junit(testResults: 'target/surefire-reports/TEST-*.xml', keepProperties: true, keepTestNames: true)
            }
        }
    }
    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}
