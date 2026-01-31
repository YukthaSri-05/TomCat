pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/YukthaSri-05/TomCat.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop azure || true
                docker rm azure || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi amazon || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t amazon .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 6060:8080 --name azure amazon'
            }
        }
    }
}
