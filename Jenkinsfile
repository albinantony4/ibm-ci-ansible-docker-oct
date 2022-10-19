pipeline {
    agent any

   // tools {
        // Install the Maven version configured as "M3" and add it to the path.
     //   maven "M3"
    //}

    stages {
        stage('scm integration') {
            steps {
               
                git credentialsId: 'git-credentials', url: 'git@github.com:albinantony4/spring-boot-chat-app.git'
            }
        }
        stage('mvn build') {
            steps {
               
              sh 'mvn -Dmaven.test.failure.ignore=true clean package'
            }
        }
        stage('unit test') {
            steps {
               
              sh 'mvn test'
              junit '**/target/surefire-reports/*.xml'
            }
        }
        stage('checkstyle') {
            steps {
               //sh 'python xunit'
              sh 'mvn checkstyle:checkstyle'
              recordIssues(tools: [checkStyle(pattern: '**/checkstyle-result.xml')])
              //junit '**/target/surefire-reports/*.xml'
            }
        }
        stage('sonar') {
            steps {
               //sh 'python xunit'
              sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=chat-app \
  -Dsonar.host.url=http://52.39.114.145:9000 \
  -Dsonar.login=sqp_ad82495e756e8e97c9e6b884b30f9bdec44228af'
              //junit '**/target/surefire-reports/*.xml'
            }
        }
        stage('nexus') {
            steps {
              nexusArtifactUploader artifacts: [[artifactId: 'websocket-demo', classifier: '', file: 'target/websocket-demo-0.0.1-SNAPSHOT.jar', type: 'jar']], credentialsId: 'nexus-credential', groupId: 'websocket-demo', nexusUrl: '35.80.219.57:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '0.0.1-SNAPSHOT'
            }
        }
    }
}

