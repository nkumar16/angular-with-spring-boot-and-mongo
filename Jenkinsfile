pipeline{
    agent any
    stages {
        stage ('BUILD') {
            steps {
                sh "mvn clean package -Dmaven.test.skip=true"
            }
        }
    } 
}
