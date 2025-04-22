pipeline {
    agent any

    tools {
        maven 'Maven_3.8.6'
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
                    script {
                        sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                        sh 'docker build -t talgatdilmurat/spring-petclinic .'
                        sh 'docker push talgatdilmurat/spring-petclinic'
                    }
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and Docker push successful!'
        }
        failure {
            echo '❌ Build failed.'
        }
    }
}
