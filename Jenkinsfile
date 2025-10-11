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
                    withCredentials([string(credentialsId: 'Docker_Hub_pwd', variable: 'Docker_Hub_pwd')]) 
                    {
                    sh 'docker push  naga123docker/dockercicd:${buildnumber}'
                    }
                }
            
            
        }
    }
    
}