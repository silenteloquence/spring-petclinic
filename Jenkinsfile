pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/silenteloquence/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Docker Build & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat 'docker login -u %DOCKER_USER% -p %DOCKER_PASS%'
                    bat 'docker build -t talgatdilmurat/spring-petclinic .'
                    bat 'docker push talgatdilmurat/spring-petclinic'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and push succeeded.'
        }
        failure {
            echo '❌ Build failed.'
        }
    }
}
