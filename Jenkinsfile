pipeline {
    agent any

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
    }
}
