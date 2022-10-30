node {
    docker.image('node:lts-buster-slim').inside('-p 3000:3000') {
        withEnv(['CI=true']) {
            stage('Install') {
                git branch: 'react-app', url: '/home/submission-cicd-pipeline-savira_nurul'
            }
            stage('Build') {
                sh 'npm install'
            }
            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
            stage('Deliver') {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}