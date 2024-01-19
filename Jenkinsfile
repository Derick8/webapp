pipeline {
 agent any
 tools {
  maven 'Maven'
 }
 stages {
    stage ('Initialize'){
      steps{
        sh '''
                echo "PATH = ${PATH}"
                echo "M2_HOME = ${M2_HOME}"
           '''
      }
    }
 stage ('Check-Git-Secretsz') {
      steps {
        sh 'rm trufflehog || true'
       sh 'whoami'
        sh 'docker run gesellix/trufflehog --json https://github.com/Derick8/webapp.git > trufflehog'
        sh 'cat trufflehog'
      }
    }
    stage ('Build') {
      steps {
           sh 'mvn clean package'
       }
    }
     stage ('Derick thing'){
      steps {
           sh 'echo "batman"'
      }
     }
  stage ('Deploy-To-Tomcat') {
            steps {
           sshagent(['tomcat']) {
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@54.79.178.76:/prod/apache-tomcat-9.0.85/webapps/webapp.war'
              }      
           }       
    }
    }
}
