
pipeline {
    agent any

    environment {
        TOMCAT_HOME = '/home/user/apache-tomcat'
        APP_NAME = 'myapp'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/USERNAME/REPOSITORY.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    cp target/*.war \
                    "$TOMCAT_HOME/webapps/$APP_NAME.war"
                '''
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }

        failure {
            echo 'Build or deployment failed!'
        }
    }
}
