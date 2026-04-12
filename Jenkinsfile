@Library("Shared") _
pipeline {
    agent {label 'car'}

    stages {
        stage("hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage('Code') {
            steps {
                script{
                    clone("https://github.com/tnxq1209/Expenses-Tracker-WebApp.git", "main")
                }
            }
        }
        stage('Build') {
            steps {
                script{
                    docker_build("expense-tracking-app", "latest", "tnxq1209")
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                script{
                    docker_push("expense-tracking-app", "latest", "tnxq1209")   
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Depolyment started.'
                sh 'docker compose down && docker compose up -d'
                echo 'App deployed.'
            }
        }
    }
}
