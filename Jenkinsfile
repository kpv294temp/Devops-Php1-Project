pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git branch: 'main', url: 'https://github.com/kpv294temp/Devops-Php1-Project.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build . -t karthick/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'docker-hub', variable: 'dockerPwd')]) {
                      sh "docker login -u karthick -p ${dockerPwd}"
                }
                
                sh "docker push karthick/my-php-website "
            }
        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

