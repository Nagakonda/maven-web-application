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
    }
    
}