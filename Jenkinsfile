pipeline {
  agent any 
  tools {
    maven 'Maven'
  }
  stages {
    stage ('Initialize') {
      steps {
        sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
            ''' 
      }
    }
    
    stage('CompileandRunSonarAnalysis') {
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          sh 'JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64/ && export JAVA_HOME & mvn -X -Dmaven.test.failure.ignore sonar:sonar -Dsonar.login=$SONAR_TOKEN -Dsonar.projectKey=webapp -Dsonar.host.url=http://localhost:9000/'
        }
      }
    }
    
    stage ('Build') {
      steps {
      sh 'mvn clean package'
       }
    }
    
  }
}
