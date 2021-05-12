pipeline{
    agent any
    stages{
        stage('SCM'){
            steps{
                git credentialsId: 'git', url: 'https://github.com/Raghu-acer/Ansible-docker.git'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        
    }
}
