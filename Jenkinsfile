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
        stage('Authenticate and Push Docker Image to AWS ECR')
        {
            steps()
            {
                sh 'aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 293578647166.dkr.ecr.ap-southeast-1.amazonaws.com'
                sh 'docker push 293578647166.dkr.ecr.ap-southeast-1.amazonaws.com/maven-web-application:${buildNumber}'
            }
        }
        stage('Remove docker image from Jenkins Server')
        {
            steps()
            {
                sh 'docker rmi 293578647166.dkr.ecr.ap-southeast-1.amazonaws.com/maven-web-application:${buildNumber}'
            }
        }
        stage('Update Image Tag in K8S Manifest File')
        {
            steps()
            {
                sh "sed -i 's/Build_Tag/${buildNumber}/g' MavenWebApplication.yaml"
            }
        }
        stage('Deploy Application in Aws EKS Cluster')
        {
            steps()
            {
                sh 'kubectl delete deployment webpage-deployment -n production || true'
                sh 'kubectl apply -f MavenWebApplication.yaml'
            }
        }
    }
}