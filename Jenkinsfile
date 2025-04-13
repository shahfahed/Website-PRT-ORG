pipeline {
    agent {
        label 'jworker'
    }
    stages {
        stage ('checkout-scm') {
            steps {
                git branch: 'main', url: 'https://github.com/shahfahed/Website-PRT-ORG.git'
            }
        }
        stage ('docker login') {
            steps {
                withDockerRegistry(credentialsId: 'docker_login', url: 'https://index.docker.io/v1/') {
                    sh 'docker build --file Dockerfile --tag shahfahed/april-prt:$BUILD_NUMBER .'
                    sh 'docker push shahfahed/april-prt:$BUILD_NUMBER'
                }
            }
        }
    }
}
