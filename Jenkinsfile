pipeline{
    agent any
    stages{
        stage('Continuous Download'){
            steps{
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Chandramouli9105/devops-automation']])
            }
        }
        stage('Continuous Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                sh 'docker build -t cmouli5019/devops-integration .'
            }
        }
        stage('Push docker Image'){
            steps{
                withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubid')]) {
                    sh 'docker login -u cmouli5019 -p ${dockerhubid}'
                }
                sh 'docker push cmouli5019/devops-integration'
            }
        }
    }
}
