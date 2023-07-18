pipeline {
    agent { label 'Dev-Agent node' }
    
    stages{
        stage('Checkout'){
            steps{
                git url: 'https://github.com/Aswini-202/Building-and-Deploying-a-Node.js-Application-with-Docker-on-Ubuntu-Using-Jenkins-CI-CD-Pipeline.git', branch: 'master'
            }
        }
        stage('Build'){
            steps{
                sh 'sudo docker build . -t aswini202/nodo-todo-app-test:latest'
            }
        }
        stage('Test image') {
            steps {
                echo 'testing...'
                sh 'sudo docker inspect --type=image aswini202/nodo-todo-app-test:latest '
            }
        }
        
        stage('Push'){
            steps{
        	     sh "sudo docker login -u basanagoudapatil -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc"
                 sh 'sudo docker push aswini202/nodo-todo-app-test:latest'
            }
        }  
        stage('Deploy'){
            steps{
                echo 'deploying on another server'
                sh 'sudo docker stop nodetodoapp || true'
                sh 'sudo docker rm nodetodoapp || true'
                sh 'sudo docker run -d --name nodetodoapp aswini202/nodo-todo-app-test:latest'
                sh '''
                ssh -i Ubuntudemo.pem -o StrictHostKeyChecking=no ubuntu@13.233.166.214 <<EOF
                sudo docker login -u aswini202 -p dckr_pat_OvN0lH_USJztUCkm0opyjz-yXNc
                sudo docker pull aswini202/nodo-todo-app-test:latest
                sudo docker stop nodetodoapp || true
                sudo docker rm nodetodoapp || true 
                sudo docker run -d --name nodetodoapp aswini202/nodo-todo-app-test:latest
                '''
            }
        }
    }
}
