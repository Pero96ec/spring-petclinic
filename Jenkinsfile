#!groovy
pipeline {
    agent none

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Pero96ec/spring-petclinic.git'
            }
        }
        
        stage('Maven Install') {
            agent {
                docker {
                    image 'maven:3.5.0'
                }
            }
            steps {
                sh 'mvn clean install'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube Scanner'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }

        stage('Docker Build') {
            agent any
            steps {
                sh 'docker build -t grupo05/spring-petclinic:latest .'
            }
        }
    }
}
