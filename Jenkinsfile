pipeline {
    agent any

    stages {

         stage('Clean container') {
            steps {
                sh 'docker rm -f cv_trinh'
            }
            post {
                success {
                    echo "====++++Container stopped and delete with success++++===="
                }
                failure {
                    echo "====++++Docker failed to stop/delete my container++++===="
                }
            }
        }

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
                sh 'docker run -d -p 8083:80 --name cv_trinh cv_trinh:1.0'
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