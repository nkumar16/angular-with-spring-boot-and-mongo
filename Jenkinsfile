pipeline {
    agent any
    environment{
        PATH = "C:\dev\apache-maven-3.6.3\bin:$PATH"
    }
    stages {
        stage('Git Checkout') {
            steps{
                   git credentialsId: 'nkumar16' , url: 'https://github.com/nkumar16/angular-with-spring-boot-and-mongo'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn package -Dmaven.Test.Skip=true'
            }
        }
    }
}
        
