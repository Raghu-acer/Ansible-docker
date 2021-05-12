pipeline{
    agent any
    
    environment {
      DOCKER_TAG = getVersion()
    }
    
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
        stage('image Build'){
            steps{
                sh "docker build . -t raghudusa/gameoflife:${DOCKER_TAG} "
            }
        }
        
    }
}
def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}
