
pipeline {
    agent any

    stages {

        stage('Git Checkout') {
            steps {
                checkout scm
                echo 'GitHub source code checked out'
            }
        }

        stage('Maven Build') {
            steps {
                bat 'mvn -B clean package'
            }
        }

        stage('Verify WAR') {
            steps {
                bat 'dir target\\apartmentsystem.war'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                bat '''
                copy /Y "target\\apartmentsystem.war" "C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0\\webapps\\apartmentsystem.war"
                '''
            }
        }
    }

    post {
        success {
            echo 'ApartmentSystem deployed successfully!'
        }

        failure {
            echo 'CI/CD pipeline failed. Check Console Output.'
        }
    }
}
