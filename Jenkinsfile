pipeline {
    agent any
    
    stages {
        stage('Clean') {
            steps {
                sh "mvn clean"
            }
        }
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package'
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }
    }
}
