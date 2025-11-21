pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('duckerhub_ziat1988')
    }

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
                sh 'docker build -t cv_trinh:1.1 .'
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
                sh 'docker run -d -p 8083:80 --name cv_trinh cv_trinh:1.1'
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

        stage ('Push image to Dockerhub') {
            steps {
                sh 'docker tag cv_trinh:1.1 ziat1988/cv_trinh:1.1'
                sh "docker login -u $DOCKERHUB_CREDENTIALS_USR -p $DOCKERHUB_CREDENTIALS_PSW"
                sh 'docker push ziat1988/cv_trinh:1.1'
                sh "docker logout"
            }
        }

    }
}