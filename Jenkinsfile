pipeline {
    agent any


    stages {
        stage('scm git') {
            steps {
                // Get some code from a GitHub repository
               git credentialsId: 'git-credentials', url: 'git@github.com:albinantony4/ansible-cd-pipeline-ibm-devops-oct221.git'
            }
        }
        stage('build') {
            steps {
                // Get some code from a GitHub repository
               sh 'mvn clean package'
            }
        }
        stage('ansible') {
            steps {
                // Get some code from a GitHub repository
               ansiblePlaybook credentialsId: 'git-credentials', disableHostKeyChecking: true, inventory: 'ansible/dev.inv', playbook: 'ansible/tomcat.yml'
            }
        }


        }
    
}


