pipeline {
    agent any
    stages {
        stage('preparation') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/hazemhashem881/Demo1.git'
            }
        }
        stage('build'){
            steps{
                sh 'docker build -t hazemhashem100/demo1 .'
            }
        }
        stage('artifact ') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                    sh 'docker login -u ${USERNAME} -p ${PASSWORD}'
                    sh 'docker push hazemhashem100/demo1'
                }
                
            }
        }
        stage('cd'){
            steps{
                sh  "docker run -d -p 3000:80 hazemhashem100/demo1"
            }
        }
        
    }
    post{
        success{
            slackSend channel: "general",color: "#439FE0", message: " Successed: ${env.JOB_NAME} ${env.BUILD_NUMBER}"
        }
    }
}

