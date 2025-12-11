pipeline
{
    agent any

    tools
    {
        maven 'Maven'
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
    }
}