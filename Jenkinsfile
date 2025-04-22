pipeline {
    agent any

    tools {
        maven 'Maven 3.8.6'  // Make sure it's exactly like this in Jenkins config
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
                script {
                    sh "docker login -u talgatdilmurat -p Tali960211"
                    sh "docker build -t talgatdilmurat/spring-petclinic ."
                    sh "docker push talgatdilmurat/spring-petclinic"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build was successful.'
        }
        failure {
            echo '❌ Build failed.'
        }
    }
}
