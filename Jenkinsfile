pipeline {
    agent 'pico'
    triggers {
        cron('5 6 * * 1-5')
    }

    options {
        checkoutToSubdirectory("source")
    }
    environment {
        PATH = "/mnt/discovery/tools/conda/bin:$PATH"
    }

    stages {
        stage("present branch") {
            echo BRANCH_NAME
        }
        stage('pytest') {
            steps {
                sh '''#!/usr/bin/env bash
                source /mnt/discovery/tools/conda/etc/profile.d/conda.sh
                conda activate firefly37
                cd source/tests; pytest --junit-xml=reports/results.xml
                '''
            }
            post {
                always {
                    archiveArtifacts artifacts: 'source/tests/reports/results.xml', fingerprint: true
                    junit  'source/tests/reports/results.xml'}
            }
        }
    }
}
