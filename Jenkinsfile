pipeline {
    agent any
    stages {
      stage ('Build') {
        steps {
          archiveArtifacts artifacts: 'dist/angularwsbam.jar'
          }
        }
    }
}
