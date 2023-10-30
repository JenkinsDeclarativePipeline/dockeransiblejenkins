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
        stage('Maven Build')
        {
            tools
            {
                maven 'mvn-3.9.5'
            }
            steps
            {
                sh 'pwd;ls -lrt'
                sh 'mvn clean package'                
            }
        }
        stage('Docker build')
        {
            /*steps
            {
                sh 'docker --version'
            }*/
            steps
            {
                script
                {
                    docker.build('uriyapraba/tomcat:0.0.1')
                }
            }
            
        }
    }
}