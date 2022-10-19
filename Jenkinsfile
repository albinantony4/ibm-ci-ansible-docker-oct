pipeline {
    environment {
        //change the ip address of registry to your registry
        registry = '35.80.219.57:8085/chatapp'
        registryCredential = 'nexus-credential'
        dockerImage = ''
    }
    agent any

   // tools {
        // Install the Maven version configured as "M3" and add it to the path.
     //   maven "M3"
    //}

    stages {
        stage('scm stage') {
            steps {
                // Get some code from a GitHub repository
             git 'https://github.com/gopal1409/springchat.git'  
            }
        }
         stage('Build') {
            steps {
                // Get some code from a GitHub repository
             sh 'mvn clean package'  
            }
        }
        stage('build image') {
            steps {
                // Get some code from a GitHub repository
                script {
                    dockerImage=docker.build registry + "$BUILD_NUMBER"
                }
            }
        }
        stage('push image') {
            steps {
                // Get some code from a GitHub repository
                script {
                    // This step should not normally be used in your script. Consult the inline help for details.
                      withDockerRegistry(credentialsId: 'nexus-credential', url: 'http://35.80.219.57:8085') {
                       dockerImage.push()
                    }
                }
            }
        }
    
    }
}
