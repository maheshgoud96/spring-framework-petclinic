pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from GitHub
                checkout([$class: 'GitSCM',
                          branches: [[name: '*/master']],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [[$class: 'CleanBeforeCheckout'], [$class: 'CleanCheckout']],
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/your-username/your-repo.git']]])
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
        
