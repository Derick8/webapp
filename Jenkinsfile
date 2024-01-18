pipeline {
 agent any
 tools {
  maven 'Maven'
 }
 stages {
    stage ('Initialize'){
      steps{
        sh '''
                echo "PATH = {PATH}"
                echo "M2_HOME = ${m@_HOME}"
           '''
      }
    }
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
  }
}
