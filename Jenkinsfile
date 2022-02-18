pipeline {
  agent {label 'slave-1'}
stages {
          stage('start') {
            steps {
              
              withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                    docker login -u ${USERNAME} -p ${PASSWORD}
                    docker build  . -t ofandoud/hello-world:latest
                    docker push ${docker-image-repo}:latest
                """
              
              
            }
            }
          }
  
}
}
