#!groovy
pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN_HOME"
    }

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/Pero96ec/spring-petclinic.git'
            }
        }

        stage('Test First') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Sonar') {
            steps {
                withSonarQubeEnv('sonarqube'){
                    sh "mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar -Pcoverage"
                }
            }
        }

        stage('Build') {
            steps {
                sh "mvn -DskipTests clean package"
            }
        }

        stage('Test') {
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
