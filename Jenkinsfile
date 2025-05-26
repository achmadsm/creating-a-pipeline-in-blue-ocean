node {
    docker.image('node:lts-alpine').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }

        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
