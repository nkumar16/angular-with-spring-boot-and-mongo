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
		withCredentials([usernamePassword(usernameVariable: 'USERNAME', passwordVariable: 'USERPASS')]) {
                    		 sshPublisher(
                        			failOnError: true,
                        			continueOnError: false,
                        			publishers:[
                           				sshPublisherDesc(
                                				configName: 'deploy',
                               	 				sshCredentials:[
                                   	 				username: "$USERNAME",
                                    					encryptedPassphrase: "$USERPASS"
                                				], 
                                				transfers:[
                                   					 sshTransfer(
                                       	 					sourceFiles: '/var/lib/jenkins/workspace/mavenproject/target/demo-0.0.1-SNAPSHOT.jar',
                                        					remoteDirectory: 'jenkins@192.168.56.105:/home/jenkins/Desktop/testfiles',
                                    						    )
                                					  ]
                           	 				         )
                        			
							   ]
					 )
					 sshPublisher(
						 publishers: [
							 sshPublisherDesc(
								 configName: 'deploy', 
								 sshCredentials: [encryptedPassphrase: '{AAAAB3NzaC1yc2EAAAADAQABAAABgQCfusWGX1zwLGrKh1SQ+XNKzjU4S+uOAz7bnkySUSuERnigCrPM3oG7SRzSqb/Nx7Er4qyBUvH9Sm+F1L2taVM8iWN326g7yHDH9AUyQBsiFOyIcT4me5eO1RzIkr4FsM/n+9sQoRBtjB5i5ZI9T66E3pjMTH/t/h1JCrL6p3PmnNW9spZj5pv/2ahe0aQ4iwQzoiIudBtyYmQ9SPea0orzaksQnVpcneOPlNdM798rTIMFRDTnjjk0EgkvjhsvncOhxoKLwneBDfbHZpAPqGyqD8Vfp1uTuxDiOvj+vwbBvckD8Hsz6KdXYz3hzZYezeuh5jz6nKz9442iE9sAvqEKFwGn4u/ckUulRHQz4WtsX/dxpc7eeqvKB9U6HG8NV9byQjvyKblgqBBrWhpQ1qVWKINT9+d1zjIHacos9JMVCP1wHNNNlFVdGTOyAN78QSX1X9P6sIj1OmG8yYo3WS6ASP6ZjvQ1TZzv4MBN6Kbhh8QEDz5Do+BcoQSh/mljJBU=}',
								 key: '', keyPath: '', username: 'jenkins'], 
								 transfers: [sshTransfer(cleanRemote: true, excludes: '', 
								execCommand: 'java -jar jenkins@192.168.56.105:/home/jenkins/Desktop/testfiles/demo-0.0.1-SNAPSHOT.jar', 
								execTimeout: 120000, 
								flatten: false, makeEmptyDirs: false, 
								noDefaultExcludes: false, patternSeparator: '[, ]+',
								remoteDirectory: 'jenkins@192.168.56.105:/home/jenkins/Desktop/testfiles/', remoteDirectorySDF: false, 
								removePrefix: 'target', 
								sourceFiles: '/var/lib/jenkins/workspace/mavenproject/target/demo-0.0.1-SNAPSHOT.jar')], 
								usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
		}
        }
    }
}
