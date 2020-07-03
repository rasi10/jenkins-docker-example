pipeline {    
    agent none
    stages {
        stage('Deploy/Build App') {
            agent {
                docker { image 'cypress/base' }
            }
            steps {
                sh '''
                    echo 'Application deployed successfully!'
                ''' 
            }
        }
        stage('Frontend tests') {
            agent {
                docker { image 'cypress/base' }
            }
            steps {
               sh '''
                    cd frontend-project/
                    npm ci && npm run test:report:regression                   
                ''' 
                archiveArtifacts allowEmptyArchive: true, artifacts: 'frontend-project/cypress/videos/**'
                publishHTML([
                    allowMissing: false, 
                    alwaysLinkToLastBuild: false, 
                    keepAll: false, 
                    reportDir: 'frontend-project/mochawesome-report', 
                    reportFiles: 'mochawesome.html', 
                    reportName: 'Frontend report', 
                    reportTitles: ''
                ])
            }
        }
    }
}