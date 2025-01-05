@Library('my-shared-library@main') _

pipeline {
    agent { label 'jenkins-slave2' }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

   stages {
        stage('Checkout Code') {
            steps {
		script {
			newfile.checkscm()
		}		
       	}
     }
        stage('Set up Java 17') {
            steps {
                script {
                	newfile.setupjava()
                }
            }
	}

        stage('Set up Maven') {
            steps {
                script {
                	newfile.mavensetup()
		}
            }
        }

        stage('Build with Maven') {
            steps {
                script {
			newfile.build()
		}
            }
        }

        stage('Upload Artifact') {
            steps {
                uploadArtifact('target/petclinic-0.0.1-SNAPSHOT.jar')
            }
        }

        stage('Run Application') {
            steps {
                script {
		newfile.runApp()
				}
            }
        }

        stage('Validate App is Running') {
          	steps {
               	script {
					newfile.validateApp()
				}
			}
        }
        stage('wait') {
			steps {
				script {
					newfile.waiting()
				}
			}
        }
        stage('stoping') {
			steps {
				script {
					newfile.stop()
				}
			}
        }
         stage('cleaning') {
			steps {
				script {
					newfile.clean()
				}
			}
        }        
    }
}
