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
    stage ('Deploy to Tomcat') {
     steps {
        sshagent(['tomcat']) {
       sh 'ssh -o  StrictHostKeyChecking=no target/*.war ubuntu@3.24.110.158:/prod/apache-tomcat-9.0.85/webapps/webapp.war'
     }
     }
    }
    }
}
