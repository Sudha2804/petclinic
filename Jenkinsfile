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
			pipeline.checkscm()
		}		
       	}
     }
        stage('Set up Java 17') {
            steps {
                script {
                	pipeline.setupjava()
                }
            }
	}

        stage('Set up Maven') {
            steps {
                script {
                	pipeline.mavensetup()
		}
            }
        }

        stage('Build with Maven') {
            steps {
                script {
			pipeline.build()
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
				pipeline.runApp()
				}
            }
        }

        stage('Validate App is Running') {
          	steps {
               	script {
					pipeline.validateApp()
				}
			}
        }
        stage('wait') {
			steps {
				script {
					pipeline.waiting()
				}
			}
        }
        stage('stoping') {
			steps {
				script {
					pipeline.stop()
				}
			}
        }
         stage('cleaning') {
			steps {
				script {
					pipeline.clean()
				}
			}
        }        
    }
}
