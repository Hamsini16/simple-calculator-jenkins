
pipeline {
    agent any

    stages {

        stage('SCM Synchronization') {
            steps {
                echo 'Pulling latest code from Git'
                checkout scm
            }
        }

        stage('Static Verification') {
            steps {
                echo 'Checking Maven project'
                bat 'mvn validate'
            }
        }

        stage('Compilation & Automated Testing') {
            steps {
                echo 'Compiling and testing'
                bat 'mvn clean package'
            }

            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }

        failure {
            echo 'CI Pipeline failed. Check console logs.'
        }
    }
}
