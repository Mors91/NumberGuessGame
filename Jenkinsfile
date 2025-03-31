pipeline {
    agent any
    tools {
        maven 'Maven'  // Ensure Maven is configured in Jenkins Global Tools
        jdk 'JDK'      // Ensure Java is configured (e.g., 'JDK11')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Mors91/NumberGuessGame.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'cp target/*.war /var/lib/tomcat/webapps/'  // Adjust path for your Tomcat server
            }
        }
    }
    post {
        failure {
            emailext body: 'Pipeline failed: ${BUILD_URL}', subject: 'Pipeline Failed', to: 'team@example.com'
        }
    }
}
