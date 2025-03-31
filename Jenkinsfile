pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([  // Replace `git` with explicit checkout
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    extensions: [
                        // Clones directly into "NumberGuessGame/" (no double nesting)
                        [$class: 'RelativeTargetDirectory', relativeTargetDir: 'NumberGuessGame']
                    ],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Mors91/NumberGuessGame.git',
                        // Use a credentials ID if your repo is private
                        credentialsId: 'github-credentials'  // Optional for public repos
                    ]]
                ])
            }
        }
        stage('Build & Test') {
            steps {
		dir('NumberGuessGame') {
                sh 'mvn clean package test'
            }
        }
	}
        stage('Deploy') {
            steps {
                sh '''
                    WAR_FILE=$(ls target/*.war)
                    echo "Deploying $WAR_FILE to Tomcat..."
                    cp "$WAR_FILE" /var/lib/tomcat/webapps/
                '''
            }
        }
    }
    post {
        failure {
            mail body: 'Pipeline failed: ${BUILD_URL}', subject: 'Pipeline Failed', to: 'snrwhyte91@yahoo.com'
        }
    }
}
