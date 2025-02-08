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
                        docker run --rm -e TARGET_HOST=${TARGET_HOST} $DOCKER_IMAGE
                    """
                }
            }
        }
    }

   post {
    always {
        emailext(
            subject: "Pipeline Status: ${env.BUILD_NUMBER}",
            body: '''<html>
                        <body>
                            <p>Build Status: ${currentBuild.currentResult}</p>
                            <p>Build Number: ${env.BUILD_NUMBER}</p>
                            <p>Check the <a href="${env.BUILD_URL}">console output</a>.</p>
                        </body>
                     </html>''',
            to: 'ditiss790@gmail.com',
            from: 'jenkins@example.com',
            replyTo: 'jenkins@example.com',
            mimeType: 'text/html'
        )
    }
}

}
