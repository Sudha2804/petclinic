@Library('my-shared-library@main') _  // Correct syntax

pipeline {
    agent { label 'jenkins-slave2' }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('checkout') {
            steps {
                script {
                 pipeLine.checkoutCode()
                }
            }
        }
        stage('setup java ') {
            steps {
                script {
                   pipeLine.setupJava17()
                }
            }
        }
        stage('setup mvn ') {
            steps {
                script {
                  pipeLine.setupMaven()
                }
            }
        }  
        stage('setup build ') {
            steps {
                script {
                   pipeLine.buildProject()
                }
            }
        }        
        stage('upload artifact ') {
            steps {
                script {
                  pipeLine.uploadArtifact('target/*.jar')
                } 
            }
        } 
        stage('run application ') {
            steps {
                script {
                  pipeLine.runSpringBootApp()
                }
            }
        } 
        stage('validate application ') {
            steps {
                script {
                   pipeLine.validateAppRunning()
                }
            }
        }
        stage('stop spring ') {
            steps {
                script {
                   pipeLine.stopSpringBootApp()
                }
            }
        }
    }
post {
        always {
            script {
                 pipeLine.cleanupProcesses()
        }
      }
   }
}
