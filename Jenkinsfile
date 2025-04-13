pipeline {
    agent any
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
        stage ('deploy to k8s') {
            steps {
                sh 'chmod 400 nv-key.pem'
                sh 'ansible-playbook -i /etc/ansible/hosts deploy.yaml -u ubuntu --private-key nv-key.pem --extra-vars "build=$BUILD_NUMBER"'
            }
        }
    }
}
