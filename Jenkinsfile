pipeline
{
    agent
    {
        node
        {
            label 'maven'
            customWorkspace '/home/jenkins/workspace/dockerjenkins'
        }
    }
    stages
    {
        stage('SCM ceckout')
        {
            steps
            {
                checkout scmGit(branches: [[name: '*/master']], 
                extensions: [], userRemoteConfigs: [[credentialsId: 'JenkinsDeclarativePipeline', 
                url: 'https://github.com/JenkinsDeclarativePipeline/dockeransiblejenkins.git']])
            }
        }
    }
}