//Owen Anderchek, A01211852
//13/04/2022
//Pipeline to run sample code for final exam
pipeline {
    agent any
    stages {

        stage('Build') {
            steps{
                sh 'echo Running the Requirements'
                sh 'pip install requirements.txt'
                sh 'echo Requirements Complete!'
            }
        }
        stage('Code Quality') { 
            steps {     
                withCredentials([string(credentialsId: 'DockerHub',variable:'TOKEN')]) { 
                    sh "docker login -u 'kingofthewestwest' -p '$TOKEN' docker.io" 
                    //fix this so it builds and pushes all of the images
                    sh "docker build -t audit:latest --tag kingofthewestwest/audit ./audit/." 
                    sh "docker push kingofthewestwest/audit" 
                    sh "docker build -t processing:latest --tag kingofthewestwest/processing ./processing/." 
                    sh "docker push kingofthewestwest/processing" 
                    sh "docker build -t receiver:latest --tag kingofthewestwest/receiver ./receiver/." 
                    sh "docker push kingofthewestwest/receiver" 
                    sh "docker build -t storage:latest --tag kingofthewestwest/storage ./storage/." 
                    sh "docker push kingofthewestwest/storage" 
                } 
            } 
        } 
        stage("Code Quantity") {
            steps {
                withCredentials([string(credentialsId: 'DockerHub',variable:'TOKEN')]) { 
                    sh "docker login -u 'kingofthewestwest' -p '$TOKEN' docker.io"
                    sh "docker manifest inspect kingofthewestwest/audit"
                    sh "docker manifest inspect kingofthewestwest/processing"
                    sh "docker manifest inspect kingofthewestwest/receiver"
                    sh "docker manifest inspect kingofthewestwest/storage"
                }
            }
        }       
      //make this work and maybe take out the params.DEPLOY
         stage("Run Scripts") {
            //when {
                //expression { params.DEPLOY }
            //}
            steps {
                //sh "docker stop ${dockerRepoName} || true && docker rm ${dockerRepoName} || true"
                //sh "docker run -d -p ${portNum}:${portNum} --name ${dockerRepoName} ${dockerRepoName}:latest"
                sshagent(credentials : ['owen-key']) {
                    //sh "ssh -o StrictHostKeyChecking=no azureuser@owen-3855-lab-6.eastus.cloudapp.azure.com docker-compose -f /home/azureuser/acit-3855-project/deployment/docker-compose.yml down"
                    sh "ssh -o StrictHostKeyChecking=no azureuser@owen-3855-lab-6.eastus.cloudapp.azure.com docker-compose -f /home/azureuser/acit-3855-project/deployment/docker-compose.yml pull"
                    sh "ssh -o StrictHostKeyChecking=no azureuser@owen-3855-lab-6.eastus.cloudapp.azure.com docker-compose -f /home/azureuser/acit-3855-project/deployment/docker-compose.yml up -d --build"
                }
            }
         }
        stage("Zip") {
            steps {
                sh "echo 1"
            }
        }
    }
}
