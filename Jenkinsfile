pipeline {
    agent any
    tools {
        maven 'Maven' // Use the Maven version configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building project...'
                sh 'mvn clean install'
            }
        }
        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                echo 'Running SonarQube analysis...'
                withSonarQubeEnv('SonarQube') { // Replace 'SonarQube' with your configured instance name
                    sh 'mvn sonar:sonar \
                        -Dsonar.projectKey=automation \
                        -Dsonar.host.url=http://<sonarqube-server-url> \
                        -Dsonar.login=<sonarqube-auth-token>'
                }
            }
        }
    }
}
