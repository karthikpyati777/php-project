pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/karthikpyati777/php-project/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t karthik854/akshatnewimg6july:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push karthik854/akshatnewimg6july:v1'
                }
            }
        }
        
     stage('Deploy') {
    steps {
        script {
            def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
            def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 karthik854/akshatnewimg6july:v1'
            
            sshagent(['sshkeypair']) {
                sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.18.90 "${dockerrm}"
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.18.90 "${dockerCmd}"
                '''
            }
        }
    }
}

    }
}
