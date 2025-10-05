pipeline {
    agent any
    tools {
        maven 'M2_HOME'
    }
     environment {
        SONARQUBE_ENV = 'SonarQubeLocal' // Match the name configured in Jenkins
    }
     stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/AyoubRebhi/devopsTP.git'
            }
        }

        stage('Build') {
            steps {
                dir('TP-Projet') { // Adjust this to match your actual folder
                    sh 'mvn clean package -DskipTests'                }
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_ENV}") {
                    dir('TP-Projet') {
                        sh 'mvn sonar:sonar -Dsonar.projectKey=TP-Projet'
                    }
                }
            }
        }

        stage('Done') {
            steps {
                echo '✅ Build and SonarQube scan completed successfully!'
            }
        }
    }
}
