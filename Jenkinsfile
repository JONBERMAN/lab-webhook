node {
    stage('Clone repository') {
        git credentialsId: 'github_access_token', url: 'https://github.com/JONBERMAN/lab-webhook.git', branch: 'main'
    }

    stage('Build image') {
        dir('docker-project-front') {
            dockerImage = docker.build("taehoon981/node-front:5.0", ".")
        }
    }

    stage('Push image') {
        withDockerRegistry([ credentialsId: "dockerhub-id", url: "" ]) {
            dockerImage.push()
        }
    }
    stage('Run Docker Compose') {
        // 필요한 경로로 이동 후 명령 실행
        sh '''
            cd /var/lib/jenkins/workspace/${JOB_NAME}/docker-project-front/RollingPaper
            docker-compose down
            docker pull taehoon981/node-front:5.0
            docker-compose up -d
        '''
    }
}

