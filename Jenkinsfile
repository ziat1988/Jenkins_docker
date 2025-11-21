pipeline {
    agent any

    stages {
        stage ('Create image docker') {
            steps {
                sh 'docker build -t cv_trinh:1.0 .'
            }
            post {
                success {
                    echo "====++++Docker image created with success++++===="
                }
                failure {
                    echo "====++++Docker image failed++++===="
                }
            }
        }

        stage ('Run container') {
            steps {
                sh 'docker run -d -p 8083:80 cv_trinh:1.0'
            }
            post {
                success {
                    echo "====++++Container started with success++++===="
                }
                failure {
                    echo "====++++Failed to start Container++++===="
                }
            }
        }

    }
}