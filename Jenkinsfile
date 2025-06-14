pipeline {
    agent any

    options {
        timestamps()
    }

    tools {
        maven 'MAVEN_HOME'  // Jenkins must have this Maven tool configured
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

        stage('Build WAR with Maven') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                bat '''
                    echo Cleaning old deployment...
                    if exist "%TOMCAT_WEBAPPS%\\MyApp.war" del /f /q "%TOMCAT_WEBAPPS%\\MyApp.war"
                    if exist "%TOMCAT_WEBAPPS%\\MyApp" rmdir /s /q "%TOMCAT_WEBAPPS%\\MyApp"
                    echo Copying new WAR...
                    copy target\\MyApp.war "%TOMCAT_WEBAPPS%\\MyApp.war"
                '''
            }
        }

        stage('Restart Tomcat') {
            steps {
                script {
                    echo 'Stopping Tomcat...'
                    def shutdownStatus = bat(script: '"%CATALINA_HOME%\\bin\\shutdown.bat"', returnStatus: true)
                    if (shutdownStatus != 0) {
                        echo "Tomcat may not be running. Shutdown returned exit code: ${shutdownStatus}"
                    }
                }
                sleep time: 3, unit: 'SECONDS'
                echo 'Starting Tomcat...'
                bat '"%CATALINA_HOME%\\bin\\startup.bat"'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline Built and Deployed Successfully!'
            echo '🌐 Visit: http://localhost:8080/MyApp/'
        }
        failure {
            echo '❌ Pipeline Failed!'
        }
    }
}
