node {
    docker.image('node:lts-alpine').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Manual Approval') {
            // Ask user to approve before continuing to Deploy stage
            input message: 'Continue to Deploy stage?', ok: 'Proceed'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'

            // Pause execution for 1 minute to keep the app running before shutdown
            echo 'App is deployed. Waiting for 1 minute before shutdown...'
            sleep time: 1, unit: 'MINUTES'

            sh './jenkins/scripts/kill.sh'
        }
    }
}
