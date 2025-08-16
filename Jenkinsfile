pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        jdk 'java17'
        maven 'Mavne3'
    }
    environment {
	    APP_NAME = "register-app-pipeline"
        RELEASE = "1.0.0"
        DOCKER_USER = "9573491127"
        DOCKER_PASS = 'docker-hub'
        IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
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
        stage("Quality Gate"){
           steps {
               script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkin-sonarqube'
                }	
            }

        }
                stage("Build & Push Docker Image") {
            steps {
                script {
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push('latest')
                    }
                }
            }

       }
     
    }
}
