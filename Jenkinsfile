pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ("Initialize") {
      steps {
          sh'''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            '''
      }
    }
      stage ("Build stage") {
          steps {
              sh 'mvn clean package'
          }
      }
    stage ("Deploy-to-tomcat") {
      steps {
        sshagent(['Tomcat']) {
          sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@34.221.62.3/:/home/tomcat/prod/apache-tomcat-
10.0.8/webapps/webapp.war'
        }
      }
    }
  }
}

