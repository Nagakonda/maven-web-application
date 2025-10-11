pipeline{
    agent any
    tools{
        maven 'maven'
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
    }
}