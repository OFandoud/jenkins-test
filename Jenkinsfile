pipeline {
  agent {label 'slave-1'}
stages {
          stage('start') {
            steps {
              script {
              withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                    echo login to dockerhub
                    docker login -u ${USERNAME} -p ${PASSWORD}
                    echo build dockerfile
                    docker build -t $DOCKER_REPO:latest .
                    echo upload to dockerhub
                    docker push $DOCKER_REPO:latest
                """
              }
              
            }
            }
          }
          stage('deploy') {
            steps {
              echo deploy 
            }
            }
          }
}
}
