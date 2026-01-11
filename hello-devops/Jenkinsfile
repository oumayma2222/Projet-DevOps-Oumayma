pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/<username>/Projet-DevOps-Oumayma.git'
            }
        }

        stage('Build & Test') {
            steps {
                sh 'mvn clean test package'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            when {
                success()
            }
            steps {
                echo 'Deploying application locally'
            }
        }

        stage('Notify Slack') {
            steps {
                slackSend channel: '#devops',
                message: "Pipeline SUCCESS: ${env.JOB_NAME}"
            }
        }
    }
}
