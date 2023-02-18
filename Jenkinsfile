pipeline {
  agent any
    tools{
        maven 'Default Maven'
    }
 stages {
  stage('SCM') {
    steps {
    checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Keerthan25/Calculator.git']])
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
