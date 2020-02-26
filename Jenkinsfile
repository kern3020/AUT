pipeline {
    agent any
    environment {
        PATH = "/mnt/discovery/tools/conda/bin:$PATH"
    }
    stages {
        stage('pytest') {
            steps {
                sh '''#!/usr/bin/env bash
                source /mnt/discovery/tools/conda/etc/profile.d/conda.sh
                conda activate firefly37
                cd tests; pytest --junit-xml=reports/results.xml
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: '${WORKSPACE}/reports/results.xml', fingerprint: true
                    junit  '${WORKSPACE}/reports/results.xml', fingerprint: true }
            }
        }	
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
}