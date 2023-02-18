peline{
    agent any
    stages{
        stage('Checkout'){
            steps{
                  checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ashaavi/sonarqubeexample.git']])                
            }
        }
        stage('Build Stage'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('Sonarqube Analysis'){
            steps{
                withSonarQubeEnv('sonarQube') {
                    sh 'mvn clean test sonar:sonar -Dsonar.projectkeys=sonartoken'
    
                }
            }
        }
    }
}
