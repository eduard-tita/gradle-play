pipeline {
    agent any
    
    stages {
        stage('Create module.xml') { 
            tools {
                jdk 'Java 8'
                gradle 'Gradle'
            }
            steps {
                sh 'gradle nexusIQIndex'                 
            }
        }
        stage('IQ Policy Evaluation') {
            steps {
                nexusPolicyEvaluation failBuildOnNetworkError: false, iqApplication: 'iq-app-01', iqStage: 'build', enableDebugLogging: false,                    
                    iqScanPatterns: [[scanPattern: 'scan-nothing']]                    
            }
        }
    }
    
    post {
        always {
            deleteDir()
        }
    }
}
