node {
    stage('Build') {
        docker.image('node:16-buster-slim').withRun('-p 3000:3000') {
            sh 'pwd && npm install'
        }
    }
    stage('Test') {
            docker.image('node:16-buster-slim').withRun('-p 3000:3000') {
            sh './jenkins/scripts/test.sh'
        }
    }
}