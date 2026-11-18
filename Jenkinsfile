
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading Railway Reservation source code'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Starting application build'
                sh '''
                test -f index.html
                test -f style.css
                test -f script.js
                echo "Application files verified successfully"
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application files'
                sh '''
                grep -qi "<html" index.html
                grep -qi "bookingForm" index.html
                grep -qi "addEventListener" script.js
                echo "All basic validation tests passed"
                '''
            }
        }

        stage('Package') {
            steps {
                echo 'Creating application package'
                sh '''
                rm -f railway-reservation.zip
                zip railway-reservation.zip index.html style.css script.js
                '''
            }
        }
    }

    post {
        success {
            echo 'Railway Reservation Build Successful!'
        }

        failure {
            echo 'Railway Reservation Build Failed!'
        }
    }
}
