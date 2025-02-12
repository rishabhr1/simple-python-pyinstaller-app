pipeline {
    agent any
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') {
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
                stash(name: 'compiled-results', includes: 'sources/*.py*')
            }
        }
        stage('Deliver') { 
            steps {
                sh "python sources/add2vals.py 2 3" 
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals' 
                }
            }
        }
    }
}
