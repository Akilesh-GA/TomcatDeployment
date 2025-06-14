pipeline {
    agent any
    options {
        timestamps()
    }
    environment {
        TOMCAT_WEBAPPS = 'D:\\Apache\\Tomcat 9\\apache-tomcat-9.0.106\\webapps'
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
        stage('Copy WAR to Tomcat') {
            steps {
                bat 'copy target\\*.war "%TOMCAT_WEBAPPS%\\MyApp.war"'
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
