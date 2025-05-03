@Library('maven-shared-library') _

pipeline {
    agent any

    tools {
        maven 'Maven 3.6.3'  
    }

    environment {
        MAVEN_HOME = tool name: 'Maven 3.6.3', type: 'Maven'
        JAVA_HOME = tool name: 'JDK 11', type: 'JDK'  
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm  
            }
        }

        stage('Build') {
            steps {
                script {
                    mavenBuild()
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'mvn test'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo 'Deploying project...'
                    sh 'mvn deploy'
                }
            }
        }
    }

    post {
        success {
            echo 'Build and deployment succeeded!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
