pipeline {
    agent any
    options {
        timestamps()
    }
    environment {
        TOMCAT_WEBAPPS = 'D:\\Apache\\Tomcat 9\\apache-tomcat-9.0.106\\webapps'
        CATALINA_HOME = 'D:\\Apache\\Tomcat 9\\apache-tomcat-9.0.106'
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
                script {
                    def shutdownStatus = bat(script: '"%CATALINA_HOME%\\bin\\shutdown.bat"', returnStatus: true)
                    if (shutdownStatus != 0) {
                        echo "Tomcat may not be running. Shutdown returned exit code: ${shutdownStatus}"
                    }
                }
                sleep time: 3, unit: 'SECONDS'
                bat '"%CATALINA_HOME%\\bin\\startup.bat"'
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline Built Successfully !!'
        }
        failure {
            echo '❌ Pipeline Build Failed !'
        }
    }
}
