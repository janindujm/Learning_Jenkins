pipeline{
    agent any
    tools {
        maven "MAVEN3.9"
        jdk "JDK17"
    }
    stages {
        stage('fetch code') {
            steps {
                git branch: 'atom', url: 'https://github.com/hkhcoder/vprofile-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn install -DskipTests'
            }
            post {
                success {
                    echo 'Archiving artifact'
                    archiveArtifacts artifacts: '**/*.war'
                }
                failure {
                    echo 'Build failed!'
                }
            }
        }

        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Checkstyle analysis') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }

        }
    }
}