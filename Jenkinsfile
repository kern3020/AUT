pipeline {
    agent any
    environment {
        PATH = "$WORKSPACE/miniconda/bin:$PATH"
    }
    stages {

        stage('setup miniconda') {
            steps {
                sh '''#!/usr/bin/env bash
                wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O miniconda.sh
                bash miniconda.sh -b -p $WORKSPACE/miniconda
                hash -r
                conda config --set always_yes yes --set changeps1 no
                conda update -q conda

                # Useful for debugging any issues with conda
                conda info -a

                conda init bash
                conda env create -f envs/conda-pequeno.yml
                '''
            }
        }
        stage('Test downloading') {
            steps {
                sh '''#!/usr/bin/env bash
                source $WORKSPACE/miniconda/etc/profile.d/conda.sh
                conda activate seeker2020
                cd tests; pytest 
                '''
            }
        }	
        stage('build') {
            steps {
                sh 'python --version'
            }
        }
    }
}