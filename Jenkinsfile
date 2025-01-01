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
                withSonarQubeEnv('SonarQube-Token-1') { // Replace 'SonarQube' with your configured instance name
                    sh '''mvn sonar:sonar \
                        -Dsonar.projectKey=AssignmentMaven \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=sqp_12db9ae249f663e21da13976b9968ab932127406'''
                }
            }
        }
    }
}
