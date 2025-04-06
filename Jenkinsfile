pipeline {
    agent any

    stages {
        stage('build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                        docker login -u $USERNAME -p $PASSWORD
                        docker build . -t omniasaad/node-jenkins:v1
                        docker push omniasaad/node-jenkins:v1
                    """
                }
            }
        }

        stage('deploy') {
            steps {
                sh """
                    docker run -d -p 3000:3000 omniasaad/node-jenkins:v1
                """
            }
        }
    }
}

