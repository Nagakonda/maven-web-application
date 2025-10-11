pipeline{
    agent any
    tools{
        maven 'maven'
    }
    environment
    {
        buildnumber = "${BUILD_NUMBER}"
    }
    stages{
        stage('Git Checkout')
        {
            steps()
            {
                git branch: 'docker_cicd', url: 'https://github.com/Nagakonda/maven-web-application.git'
            }
        }
        stage('Build Project Artifact using Maven')
        {
            steps()
            {
                sh 'mvn clean package'
            }
        }
        stage('Build the docker image')
        {
            steps()
            {
            sh 'docker build -t naga123docker/dockercicd:${buildnumber} .'
            }
        }
        stage('Push Docker image to Docker Registry')
        {
            steps()
                {
                    withCredentials([string(credentialsId: 'Docker_Hub_Pwd', variable: 'Docker_Hub_Pwd')]) 
                    {
                    sh 'docker login -u naga123docker -p ${Docker_Hub_Pwd}'
                    }
                    sh 'docker push naga123docker/dockercicd:${buildnumber}'
                }
        }
        stage('Remove Docker Image Locally')
        {
            steps()
            {
                sh 'docker rmi naga123docker/dockercicd:${buildnumber}'
            }
        }
        stage('Deploy Application to Docker Deployment Server')
        {
            steps()
            {
                sshagent(['DeployamentServer_SSH']) 
                {
                sh "ssh -o StrictHostKeyChecking=no ubuntu@13.215.178.228 docker rm -f mavenwebapplication || true" 
	            sh "ssh -o StrictHostKeyChecking=no ubuntu@13.215.178.228 docker run -d --name mavenwebapplication -p 8080:8080 naga123docker/dockercicd:${buildnumber}"   
                }
            }
        }
    }
    
}