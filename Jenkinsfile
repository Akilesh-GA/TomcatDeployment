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
        stage('Copy WAR to Tomcat') {
            steps {
                bat 'copy target\\*.war "%TOMCAT_WEBAPPS%\\MyApp.war"'
            }
        }
        stage('Restart Tomcat') {
            steps {
                bat '"D:\\Apache\\Tomcat 9\\apache-tomcat-9.0.106\\bin\\shutdown.bat"'
                sleep time: 3, unit: 'SECONDS'
                bat '"D:\\Apache\\Tomcat 9\\apache-tomcat-9.0.106\\bin\\startup.bat"'
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
