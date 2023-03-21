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
                sh 'docker build . -f dockerfile -t hazemhashem100/demo1'
            }
        }
        stage('ci') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_hub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')])
                sh '''
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker push hazemhashem100/demo1
                '''
            }
        }
        stage('cd'){
            steps{
                sh  "docker run -d -p 3000:3000 hazemhashem100/demo1"
            }
        }
    }
}
