pipeline {
    agent any
    tools {
        maven 'Maven' // Name you configured in Jenkins
    }
    environment {
        //SONAR_TOKEN = credentails('SonarQube-Token-1')
        SONAR_SCANNER_PATH = 'C:\\Program Files\\sonar-scanner-cli-6.2.1.4610-windows-x64\\sonar-scanner-6.2.1.4610-windows-x64\\bin\\sonar-scanner.bat'// Add this line
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/riti-1904/AssignemntMaven' // Replace with your repo URL
            }
        }
        stage('Build and Analyze') {
             environment {
                SONAR_TOKEN = credentials('SonarQube-Token-1')
            }
            steps {
                bat """
                    // mvn clean verify sonar:sonar -X ^
                    // -Dsonar.projectKey=MavenProject ^
                    // -Dsonar.projectName=MavenProject ^
                    // -Dsonar.sources=. ^
                    // -Dsonar.host.url=http://localhost:9000 ^
                    // -Dsonar.token=%SONAR_TOKEN% ^
                    // -Dsonar.verbose=true

  mvn clean verify sonar:sonar \
  -Dsonar.projectKey=AssignmentMaven \
  -Dsonar.projectName='AssignmentMaven' \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.token=sqp_12db9ae249f663e21da13976b9968ab932127406


                """
            }
        }
    }
    post {
        success {
            echo 'Build and analysis completed successfully!'
        }
        failure {
            echo 'Build or analysis failed!'
        }
        always {
            echo 'This will always run, regardless of success or failure.'
        }
    }
}
