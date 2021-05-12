pipeline{
    agent any

    environment {
      DOCKER_TAG = getVersion()
    }
    stages{
        stage('SCM'){
            steps{
                git 'https://github.com/Raghu-acer/anisble-docker-deploy.git'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh "mvn clean package"
            }
        }
        
        stage('Docker Build'){
            steps{
                sh "docker build . -t raghudusa/gameoflife:${DOCKER_TAG} "
            }
        }
        
        stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'raghudusa', variable: 'dockerhub')]) {
                    sh "docker login -u raghudusa -p ${dockerhub}"
                }
                
                sh "docker push raghudusa/gameoflife:${DOCKER_TAG} "
            }
        }
        
        stage('Docker Deploy'){
            steps{
              ansiblePlaybook credentialsId: 'ansible', disableHostKeyChecking: true, extras: 'DOCKER_TAG', installation: 'Ansible', inventory: 'dev.inv', playbook: 'deploy-docker.yml'
            }
        }
    }
}

def getVersion(){
    def commitHash = sh label: '', returnStdout: true, script: 'git rev-parse --short HEAD'
    return commitHash
}