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
            docker tag image:$BUILD_ID projectsunique.jfrog.io/docker-trial/image:$BUILD_ID
            docker push projectsunique.jfrog.io/docker-trial/image:$BUILD_ID
        }
    }
}
}