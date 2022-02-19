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
                withSonarQubeEnv(credentialsId: '6b05758ea8627c9c644c62aba55cbede16c180b1', installationName: 'SonarQube-Token') {
                sh 'mvn sonar:sonar'
                }                
            }
        }
    }
}