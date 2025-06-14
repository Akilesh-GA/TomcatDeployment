pipeline {
    agent any
    options {
        timestamps()
    }
    tools {
        maven 'MAVEN_HOME'
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
