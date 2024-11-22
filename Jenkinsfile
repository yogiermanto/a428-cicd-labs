node {
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        try {
            stage('Checkout') {
                // Pastikan kode di-clone dari repository
                checkout scm
            }

            stage('Build') {
                // Jalankan npm install
                sh 'npm install'
            }

            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
        } catch (Exception e) {
            error "Pipeline failed: ${e.message}"
        }
    }
}