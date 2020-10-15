pipeline {
    agent any
    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }
    stages {
        stage ('SCM Checkout') {
            steps {
            git 'https://github.com/nkumar16/angular-with-spring-boot-and-mongo'
        }
        }
        stage ('compile-package') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               junit allowEmptyResults: true, testResults: '*/target/surefire-reports/TEST-.xml'
               archiveArtifacts 'target/*.jar'
               }
         }
      }
 	stage ('copy artifact') {
	steps {
        sh "scp qmaster@13.68.169.106:/home/qmaster/testfiles/ /var/lib/jenkins/workspace/mavenproject/target/demo-0.0.1-SNAPSHOT.jar"		
	   }
}
   }
}
