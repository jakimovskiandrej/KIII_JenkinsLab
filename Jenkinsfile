pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                git credentialsId: 'github-creds', url: 'https://github.com/jakimovskiandrej/KIII_JenkinsLab.git'
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t jakimovskiandrej/kiii-jenkinslab:latest .'
            }
        }

        stage('Push image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push jakimovskiandrej/kiii-jenkinslab:latest'
                }
            }
        }
    }
}