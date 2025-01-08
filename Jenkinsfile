node {
    stage('Clone repository') {
        git credentialsId: 'github-access', url: 'https://github.com/JONBERMAN/lab-webhook.git'
    }

    stage('Build image') {
        dir('docker-project-front') {
            dockerImage = docker.build("taehoon981/node-front:3.0")
        }
    }

    stage('Push image') {
        withDockerRegistry([ credentialsId: "dockerhub-id", url: "" ]) {
            dockerImage.push()
        }
    }
}

