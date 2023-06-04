pipeline {
    agent {
            label 'vagrant'
          }
    stages {
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t lesson38-docker .'
                }
            }
        }
        stage('Run') {
            steps {
                sh 'docker run -d -p 8000:8000 --name lesson38-docker lesson38-docker gunicorn --bind 0.0.0.0:8000 src.core.wsgi:app'
            }
        }

        stage('Test') {
            steps {
                sh 'ip ad'
                sh 'curl 192.168.56.3:80'
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('http://192.168.16.4:5000') {
                        docker.image('lesson38-docker').push()
                    }
                }
            }
        }
        stage('clean') {
            steps {
                sh 'docker stop lesson38-docker && docker rm lesson38-docker'
            }
        }

    }
    post {
        failure {
            sh 'docker stop lesson38-docker && docker rm lesson38-docker'
        }
        always {
            sh 'docker rmi lesson38-docker'
        }
    }
}
