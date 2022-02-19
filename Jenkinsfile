pipeline{
    agent any
    environment {
        PATH = "$PATH:/usr/share/maven"
    }
    stages
    {
        stage ('Checkout From SCM')
        {
            steps
            {
              checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/javaloginapp.git']]])
            }
        }
        stage ('BUILD')
        {
            steps{
                sh 'mvn clean package'
            }
        }
        stage ('SonarQube Analysis')
        {
            steps{
                withSonarQubeEnv('SonarQube8.9.2') {
                sh 'mvn sonar:sonar'
                }                
            }
        }
    }
}