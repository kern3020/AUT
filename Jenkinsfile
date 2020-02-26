pipeline {
    agent {
        node {
            label 'custom'
            customWorkspace 'source'
        }
    }
    triggers {
        cron('5 6 * * 1-5')
    }

    environment {
        PATH = "/mnt/discovery/tools/conda/bin:$PATH"
    }
    stages {
        stage("setup worksapce") {
            steps {
                sh'''#!/usr/bin/env bash
                # create well known directories

                # create well known links

                '''
            }
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