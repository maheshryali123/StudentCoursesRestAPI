pipeline {
    agent { label 'DEV'}
    triggers { pollSCM('* * * * *') }
    stages {
        stage('clone the code') {
            steps {
                git branch: 'dev',
                       url: 'https://github.com/maheshryali123/StudentCoursesRestAPI.git'
            }
        }
        stage('Install the requirements') {
            steps {
                sh ' pip install -r requirements.txt '
            }
        }
        stage('Docker image build') {
            steps {
                sh 'docker image build -t image:$BUILD_ID .'
            }
        }
        stage('push to jfrog') {
            steps {
            rtDockerPush(
                serverId: "jfrogserver",
                image: "52.55.76.200:8081/docker-virtual/image:$BUILD_ID",
                targetRepo: 'local-repo', // where to copy to (from docker-virtual)
                // Attach custom properties to the published artifacts:
                properties: 'project-name=docker1;status=stable'
            )
        }
        }
    }
}