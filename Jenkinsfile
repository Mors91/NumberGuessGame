pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
		dir ('subdirectory-with-pom') {
                git 'https://github.com/Mors91/NumberGuessGame.git'
            }
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
            mail body: 'Pipeline failed: ${BUILD_URL}', subject: 'Pipeline Failed', to: 'snrwhyte91@yahoo.com'
        }
    }
}
