pipeline {
    agent any
    
 
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
