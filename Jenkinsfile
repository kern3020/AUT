pipeline {
    agent any
    triggers {
        cron('5 6 * * 1-5')
    }
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
                    archiveArtifacts artifacts: 'tests/reports/results.xml', fingerprint: true
                    junit  'tests/reports/results.xml'}
            }
        }	
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
}