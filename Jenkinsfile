#!groovy
pipeline {
    agent any

    tools {
        maven "MAVEN_HOME"
    }

    stages {
        stage('Test') {
            steps {
                    sh "mvn clean test"
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

        stage('Docker Build') {
            agent any
            steps {
                sh 'docker build -t grupo05/spring-petclinic:latest .'
            }
        }
    }
}
