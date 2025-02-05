pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nmap-python:latest'  // Define the Docker image name
        TARGET_HOST = 'cmet.gov.in'          // Define the target for the Nmap scan
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container and pass the target as an environment variable
                    sh """
                        docker run --rm -e TARGET_HOST=$TARGET_HOST $DOCKER_IMAGE
                    """
                }
            }
        }
    }

    post {
        always {
            // Clean up the Docker images after running the job
            sh 'docker rmi $DOCKER_IMAGE || true'
        }
    }
}
