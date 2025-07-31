pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Clone') {
            steps {
                git credentialsId: 'remote-ssh', url: 'https://github.com/vinsen007/devops-ci-cd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:$IMAGE_TAG .'
            }
        }

        stage('Save Docker Image as Tar') {
            steps {
                sh 'docker save $IMAGE_NAME:$IMAGE_TAG -o myapp.tar'
            }
        }

        stage('Run Ansible Deployment') {
            steps {
                sh 'ansible-playbook -i inventory deploy.yml'
            }
        }
    }
}

