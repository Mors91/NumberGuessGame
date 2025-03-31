pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
		dir ('NumberGuessGame') {
                git 'https://github.com/Mors91/NumberGuessGame.git'
            }
        }
	}
        stage('Build & Test') {
            steps {
		dir('NumberGuessGame') {
                sh
		  'mvn clean package test'
            }
        }
	}
        stage('Deploy') {
            steps {
                sh 'sudo cp target/*.war /var/lib/tomcat/webapps/'  // Adjust path for your Tomcat server
            }
        }
    }
    post {
        failure {
            mail body: 'Pipeline failed: ${BUILD_URL}', subject: 'Pipeline Failed', to: 'snrwhyte91@yahoo.com'
        }
    }
}
