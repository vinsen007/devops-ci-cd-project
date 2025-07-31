pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "flask-app"
        DOCKER_IMAGE_TAG = "latest"
        DOCKER_IMAGE_TAR = "flask-app.tar"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',   // <-- was 'master', changed to 'main'
                credentialsId: 'remote-ssh',
                url: 'https://github.com/vinsen007/devops-ci-cd-project.git'

            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE_NAME:$DOCKER_IMAGE_TAG .'
            }
        }

        stage('Save Docker Image as Tar') {
            steps {
                sh 'docker save $DOCKER_IMAGE_NAME:$DOCKER_IMAGE_TAG -o $DOCKER_IMAGE_TAR'
            }
        }

        stage('Run Ansible Deployment') {
            steps {
                sh 'ansible-playbook -i ansible/inventory ansible/deploy_flask_app.yml'
            }
        }
    }
}
