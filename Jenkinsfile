pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'java17'
        maven 'Mavne3'
    }
    stages {
        stage('clean the workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Checkout') {
            steps {
               git(
                    branch: 'main',
                    credentialsId: 'github',
                    url: 'https://github.com/Anuragsaroj/project_1_register-app.git'
                )
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
        stage('sonarqube analysis') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'jenkin-sonarqube') {
                        sh 'mvn sonar:sonar'
                    }
                }
                
        }
    }
     
}
}
