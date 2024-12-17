pipeline {
    agent any

    stages {
        stage('Git checkout') {
            steps {
                echo "Checking out the code from SCM"
                checkout scm
                sleep 1
            }
        }

        stage('Sending Dockerfile to Ansible server') {
            steps {
                echo "Sending Dockerfile to the Ansible server"
                sleep 1
            }
        }

        stage('Docker build image') {
            steps {
                echo "Building Docker image"
                sh 'docker build -t my-image:latest .'
                sleep 2
            }
        }

        stage('Push docker images to DockerHub') {
            steps {
                echo "Pushing Docker image to DockerHub"
                sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                sh 'docker push my-image:latest'
                sleep 2
            }
        }

        stage('Copy files from Jenkins to Kubernetes server') {
            steps {
                echo "Copying files from Jenkins to the Kubernetes server"
                sh 'scp Dockerfile user@kubernetes-server:/path/to/destination'
                sleep 1
            }
        }

        stage('Kubernetes deployment using Ansible') {
            steps {
                echo "Deploying application to Kubernetes using Ansible"
                sh 'ansible-playbook -i inventory deploy.yml'
                sleep 20
            }
        }
    }

    post {
        success {
            echo "Pipeline executed successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
