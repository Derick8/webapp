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
       sh 'mvn package'
       sh 'mvn dependency:resolve-plugins'
       sh 'mvn clean package'
       }
  }
}
}
