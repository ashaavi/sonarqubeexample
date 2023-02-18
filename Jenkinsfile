pipeline{
    agent any
     tools{
          maven 'maven'
     }
    stages{
        stage('SCM'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ashaavi/sonarqubeexample.git']])
                
            }
        }
         stage('SonarQube Analysis'){
           
            steps{
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn clean test sonar:sonar -Dsonar.projectkey=sonar-token'
                }
            }
         }
         stage('Quality Gate'){
             steps{
                 timeout(time: 1, unit: 'HOURS'){
                     waitForQualityGate abortPipeline: true
                 }
             }
         }
         stage('Build'){
            steps{
                sh 'mvn clean install'
            }
         }
    }
}

