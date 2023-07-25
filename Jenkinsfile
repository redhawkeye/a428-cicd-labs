node {
    checkout scm
    docker.image('node:16-buster-slim').inside("""-p 0.0.0.0:3000:3000""") {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input(message: "Lanjutkan ke tahap Deploy?")
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
            // input(message: 'Finished using the web site? (Click "Proceed" to continue)')
            sh 'sleep 60'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
