pipeline {
    agent any
    stages {
        stage('preparation') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/hazemhashem881/Demo1.git'
            }
        }
        stage('docker build image'){
            steps{
                sh 'docker build -t hazemhashem100/demo1 .'
            }
        }
        stage('push image to hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhup-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u hazemhashem100 -p ${dockerhubpwd}'
                }
                
                
                sh 'docker push hazemhashem100/demo1'
                
            }
        }
        stage('cd'){
            steps{
                sh  "docker run -d -p 3000:3000 hazemhashem100/demo1"
            }
        }
    }
}
