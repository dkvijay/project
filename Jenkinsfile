pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/dkvijay/project/', branch: "master"
                sh 'mvn clean package'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t dkvijay/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -U $USER --password-stdin"
                    sh 'docker push dkvijay/staragileprojectfinance:v1'
                }
            }
        }
        
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 dkvijay/staragileprojectfinance:v1'
                    
                }
            }
        
    }
}
