pipeline {
    agent any
    stage('BUILD') {
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }
    } 
