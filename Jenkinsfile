pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Mors91/NumberGuessGame.git'
            }
        }
        stage('Build & Test') {
            steps {
                sh '''
		    # verify Java/Maven exist
                    java -version
		    mvn -version
	            mvn clean package test
		'''
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
            emailext body: 'Pipeline failed: ${BUILD_URL}', subject: 'Pipeline Failed', to: 'team@example.com'
        }
    }
}
