pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Tarrshan02/simple-servlet-demo.git'
            }
        }

        stage('Build WAR') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy WAR') {
            steps {
                bat '''
                if exist "C:\\Tomcat10\\webapps\\simple-servlet-demo" rmdir /s /q "C:\\Tomcat10\\webapps\\simple-servlet-demo"
                if exist "C:\\Tomcat10\\webapps\\simple-servlet-demo.war" del /f /q "C:\\Tomcat10\\webapps\\simple-servlet-demo.war"
                copy /Y "target\\simple-servlet-demo.war" "C:\\Tomcat10\\webapps\\simple-servlet-demo.war"
                '''
            }
        }

        stage('Restart Tomcat') {
            steps {
                bat '''
                net stop Tomcat10
                timeout /t 5 /nobreak
                net start Tomcat10
                '''
            }
        }
    }
}