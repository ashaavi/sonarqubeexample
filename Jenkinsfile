pipeline {
  agent any
    tools{
        maven 'maven'
    }
 stages {
  stage('SCM') {
    steps {
    checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ashaavi/sonarqubeexample.git']])
  }
  }
     stage('SonarQube Analysis') {
    steps {
    withSonarQubeEnv(installationName: 'sonarQube') {
      sh "mvn clean test sonar:sonar -Dsonar.projectKey=sonartoken"
    }
  }
 }
  stage('Quality Gate') {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }        
}
}
