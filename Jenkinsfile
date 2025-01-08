node {
    stage('Clone repository') {
        git credentialsId: 'github_access_token', url: 'https://github.com/JONBERMAN/lab-webhook.git', branch: 'main'
    }

    stage('Build image') {
        dir('docker-project-front') {
            sh 'ls -l'
            dockerImage = docker.build("taehoon981/node-front:3.0", ".")
        }
    }

    stage('Push image') {
        withDockerRegistry([ credentialsId: "dockerhub-id", url: "" ]) {
            dockerImage.push()
        }
    }
}

