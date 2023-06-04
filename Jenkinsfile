pipeline {
    agent {
            label 'vagrant'
          }
        }
        stage('Build') {
            steps {
                script {
                    sh 'docker build -t lesson38-docker .'
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
                    docker.withRegistry('http://192.168.16.4:5000') {
                        docker.image('lesson38-docker').push()
                    }
                }
            }
        }
    }
}

