pipeline {
    agent any
    
    environment {
        MAVEN_HOME = tool name: 'Maven', type: 'hudson.tasks.Maven$MavenInstallation'
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/main']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'CleanCheckout']],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/maheshgoud96/spring-framework-petclinic.git']]])
            }
        }

        stage('Install Maven') {
            steps {
                // Install and configure Maven
                script {
                    def MAVEN_HOME = tool name: 'Maven', type: 'hudson.tasks.Maven$MavenInstallation'
                    env.PATH = "${mvnHome}/bin:${env.PATH}"
                }
            }
        }
        stage('Build') {
            steps {
                // Build the WAR file (replace 'mvn' with your build tool)
                sh 'mvn clean package'
                
                // Archive the WAR file for later deployment
                archiveArtifacts artifacts: '**/target/*.war', allowEmptyArchive: true
            }
        }
    }
}
