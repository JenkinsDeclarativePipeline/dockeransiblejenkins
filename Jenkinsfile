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
    environment
    {
        docker_tag = getVersion()
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
                /*script
                {
                    docker.build('uriyapraba/tomcat:"${docker_tag}"')
                }*/
                sh "docker build . -t uriyapraba/tomcat:${docker_tag}"
            }   
        }
        stage('Docker Push')
        {
            agent
            {
                docker
                {
                    image "uriyapraba/tomcat:${docker_tag}"
                    //label 'docker'
                    registryUrl 'https://quay.io/'
                    registryCredentialsId 'quay.io'
                }
            }
            steps
            {
                sh "docker push uriyapraba/tomcat:${docker_tag}"
                echo "===Pushing docker image success====="
            }
            
            /*steps
            {               
                withCredentials([string(credentialsId: 'dockerhub_secret', variable: 'docker_secret')]) 
                {
                    sh "docker login -u uriyapraba -p ${docker_secret}"
                }
                    sh "docker push uriyapraba/tomcat:${docker_tag}"   
            }*/
        }
    }
}
//Getting commitID short head and retrun the value to environment for docker build image
def getVersion()
{
   def commitHash = sh returnStdout: true, script: 'git rev-parse --short HEAD'
   return commitHash
}

/*agent
            {
                docker
                {
                    image "uriyapraba/tomcat:${docker_tag}"
                    //label 'docker'
                    registryUrl 'https://quay.io/'
                    registryCredentialsId 'quay.io'
                }
            }
            steps
            {
                echo "===Pushing docker image success====="
            }*/

 /*withDockerRegistry(credentialsId: 'docker_hub', url: 'https://hub.docker.com/') 
                {
                    sh "docker push uriyapraba/tomcat:${docker_tag}" 
                }*/