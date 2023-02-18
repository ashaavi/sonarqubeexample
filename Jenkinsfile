pipeline{
    agent any
    stages{
        stage('SCM'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ashaavi/sonarqubeexample.git']])
                
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('SonarQube Analysis'){
            steps{
                withSonarQubeEnv(InstallationName: 'sonarqube') {
                    sh 'mvn clean test sonar:sonar -Dsonar.projectKey=sonar-token'
    
                }
            }
        }
        
    }
}
