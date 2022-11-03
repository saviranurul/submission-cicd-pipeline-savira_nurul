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
            stage('Manual Approval') {
                input message: 'Lanjutkan ke tahap Deploy? (Pilih "Proceed" untuk melanjutkan eksekusi pipeline, atau Pilih "Abort" untuk menghentikan eksekusi pipeline.)'
            }
            stage('Deploy') {
                sh './jenkins/scripts/deliver.sh'
                sleep time: 1, unit: 'MINUTES'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}