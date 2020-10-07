pipeline{
    agent any
    stages {
        stage ('BUILD') {
            steps {
                sh "mvn package -Dmaven.test.skip=true"
            }
        }
    } 
}
