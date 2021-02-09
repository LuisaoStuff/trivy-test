#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {
        IMAGE = 'debian:10.8'
    }
    stages {
        stage('trivy') {
            steps {
                sh 'trivy image --format json --output trivy-results.json ${IMAGE}'
            }        
            post {
                always {
                    recordIssues enabledForFailure: true, tool: trivy(pattern: 'trivy-results.json')
                }
            }
        }
    }
}
