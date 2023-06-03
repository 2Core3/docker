pipeline {
    agent {dockerfile true}
    stages {
        stage('Build') {
            steps {
                script {
                    docker.build('lesson38-docker')
                }
            }
        }
        stage('Run') {
            steps {
                sh 'docker run -d -p 80:80 --name lesson38-docker lesson38-docker'
            }
        }

        stage('Test') {
            steps {
                sh 'curl 192.168.56.3:80'
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry('http://172.30.0.5":5000') {
                        docker.image('lesson38-docker').push()
                    }
                }
            }
        }
        stage('clean') {
            steps {
                sh 'docker stop lesson38-docker'
                sh 'docker rm lesson38-docker'
            }
        }

    }
    post {
        failure {
            sh 'docker stop lesson38-docker'
            sh 'docker rm lesson38-docker'
        }
        always {
            sh 'docker image rm lesson38-docker'
        }
    }
}
