#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('trivy') {
            steps {
                sh 'trivy image --format json --output trivy-results.json debian:latest'
            }        
            post {
                always {
                    recordIssues enabledForFailure: true, tool: trivy(pattern: 'trivy-results.json')
                }
            }
        }
    }
}
