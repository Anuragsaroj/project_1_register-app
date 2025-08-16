pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    stages {
        stage('clean the workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout') {
            steps {
                git brach 'main', credentialsId: 'github', url: https://github.com/Anuragsaroj/project_1_register-app.git'
            }
        }
        stage('Build Appklication') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tes Application') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn deploy'
            }
        }
    }
     
}
