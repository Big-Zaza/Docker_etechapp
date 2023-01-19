pipeline {
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    agent any
    tools {
        maven "maven"
    }
    
    stages {
        stage('checkout') {
        steps {
            git branch: 'master', url: 'https://github.com/Big-Zaza/Docker_etechapp.git'
        }
	}
        stage('Docker build') {
            steps{ 
            sh "docker build -t docker/getting-started ."            
            }
        }
         stage('Image backup to ECR') {
            steps{
            sh "docker tag test/team4:latest 252316791856.dkr.ecr.us-east-1.amazonaws.com/test/team4:latest"
            sh "docker push 252316791856.dkr.ecr.us-east-1.amazonaws.com/test/team4:latest"
            }
        }
        stage('Run Docker container on Jenkins Agent') {   
            steps{
                sh "docker run -d -p 8008:8080 docker/getting-started"
            }
        }
        
        }
    }


