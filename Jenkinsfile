pipeline {
    agent any
    
    stages {
        stage ('SCM Checkout') {
            git 'https://github.com/nkumar16/angular-with-spring-boot-and-mongo'
        }
        stage ('compile-package') {
            steps {
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit '**/target/surefire-reports/TEST-*.xml'
               archiveArtifacts 'target/*.jar'
            }
         }
      }
   }
}
