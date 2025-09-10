pipeline {
    agent any
      environment {
        DOCKER_IMAGE = 'anirudev/apachewebsite:latest'
    }

    stages {
        stage('Clone Git repository') {
            steps {
                 git 'https://github.com/RaksAniruddha/apachewebsite.git'
            }
        }
        stage('run ansibleplaybook'){
          steps{
            ansiblePlaybook credentialsId: 'ansible-ssh', installation: 'ansible2', inventory: 'inventory.ini', playbook: 'installapche.yml', vaultTmpPath: ''
          }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'docker', toolName: 'docker') {
                        sh ''' 
                        echo "Building Docker image..."
                        docker build --no-cache -t $DOCKER_IMAGE -f apachewebsite/Dockerfile apachewebsite
                        echo "Pushing Docker image to Docker Hub..."
                        docker push $DOCKER_IMAGE
                        '''
                    }
                }
            }
        }

    }
}

