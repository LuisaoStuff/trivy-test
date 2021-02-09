#!/usr/bin/env groovy

pipeline {
    stages {
        stage ('trivy') {
            script {
                sh 'trivy image --format json --output trivy-results.json debian:latest'
            }        
        }
        post {
            always {
                recordIssues enabledForFailure: true, tool: trivy(pattern: 'trivy-results.json')
            }
        }
    }
}
