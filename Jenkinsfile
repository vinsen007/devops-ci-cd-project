pipeline {
    agent any

    environment {
        IMAGE_NAME = 'flask-app'
        IMAGE_TAG = 'latest'
        TAR_NAME = 'flask-app.tar'
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', credentialsId: 'remote-ssh', url: 'https://github.com/vinsen007/devops-ci-cd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .'
            }
        }

        stage('Save Docker Image as Tar') {
            steps {
                sh 'docker save -o ${TAR_NAME} ${IMAGE_NAME}:${IMAGE_TAG}'
                sh 'mv ${TAR_NAME} ansible/'
            }
        }

        stage('Run Ansible Deployment') {
            steps {
                dir('ansible') {
                    sh 'ansible-playbook -i inventory deploy_flask_app.yml'
                }
            }
        }
    }
}
