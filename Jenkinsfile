pipeline {
    agent any
    options {
        timestamps()
    }
    tools {
        maven 'Maven 3.9.10'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Akilesh-GA/TomcatDeployment.git', branch: 'main'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline Built Successfully !!'
        }
        failure {
            echo '❌ Pipeline Built Failed !'
        }
    }
}
