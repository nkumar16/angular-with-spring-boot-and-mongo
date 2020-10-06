pipeline {
    agent any
    environment {
        PATH = "C:\dev\apache-maven-3.6.3\bin:$PATH
    }
    stages {
        stage('clean') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('package') {
            steps {
                sh 'mvn package -Dmaven.test.skip=true'
            }
        }
    }   
}
