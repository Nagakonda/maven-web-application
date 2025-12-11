pipeline
{
    agent any

    tools
    {
        maven 'Maven'
    }
    environment
    {
        buildNumber = "${BUILD_NUMBER}"
    }
    
    stages
    {
        stage('Checkout Code from GitHub')
        {
            steps()
            {
                git branch: 'K8SNEW', url: 'https://github.com/Nagakonda/maven-web-application.git'
            }
        }
        stage('Build Artifact')
        {
            steps()
            {
                sh 'mvn clean package'
            }
        }
        stage('Build Docker Image')
        {
            steps()
            {
            sh 'docker build -t 293578647166.dkr.ecr.ap-southeast-1.amazonaws.com/maven-web-application:${buildNumber} .'
            }
        }
    }
}