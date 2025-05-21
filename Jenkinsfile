pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    tools {
        maven 'maven'
        jdk 'java'
    }

    stages {
        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t sharonkumar/finance-me-app:v1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-creds']) {
                    sh 'docker push sharonkumar/finance-me-app:v1'
                }
            }
        }
    }
}
