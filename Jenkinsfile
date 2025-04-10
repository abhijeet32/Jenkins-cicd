pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/abhijeet32/jenkins-cicd']])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                    sh 'docker build -t abhi0874/jenkins-cicd .'
                    echo 'Image Building is Complete'
                }
            }
        }
        stage('Push Docker Image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u abhi0874 -p ${dockerhubpwd}'
}
                    sh 'docker push abhi0874/jenkins-cicd'
                    echo 'Image Pushed to Docker Hub'
                }
            }
        }
    }
}