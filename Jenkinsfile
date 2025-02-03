pipeline {
    agent any

    stages {
        stage('Run Nmap Scan') {
            steps {
                sh 'nmap -F scanme.nmap.org > nmap_results.txt'
            }
        }

        stage('Show Results') {
            steps {
                sh 'cat nmap_results.txt'
            }
        }
    }
}
