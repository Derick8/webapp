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
  stage ('Source compisition analysys - OWASP dependancy check') {
   steps {
    sh 'rm owasp* || true'
     sh 'wget https://raw.githubusercontent.com/Derick8/webapp/master/owasp-dependency-check.sh'
    sh 'chmod +x owasp-dependency-check.sh'
    sh './owasp-dependency-check.sh -e 1503d4d0-892f-4204-9fa6-f3e263e7b1bf'
    sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-repor.xml'
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
                sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@13.211.11.110:/prod/apache-tomcat-9.0.85/webapps/webapp.war'
              }      
           }       
    }
    }
}
