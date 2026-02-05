pipeline {
    agent any

    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Checkout Source') {
            steps {
                git url: 'https://github.com/S-Swathii/quality-gate-demo.git',
                    branch: 'main'
            }
        }

        stage('Build and Test') {
            steps {
                echo 'Starting Maven Build and Running Unit Tests'
                sh 'mvn clean package'
            }
        }

        stage('Quality Gates and Archival') {
            steps {
                junit 'target/surefire-reports/*.xml'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        failure {
            echo 'CI Pipeline Failed.'
        }
    }
}
