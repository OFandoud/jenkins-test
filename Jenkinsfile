pipeline {
  agent {label 'slave-1'}
stages {
          stage('start') {
            steps {
              script {
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
          stage('deploy') {
            steps {
              script {
              withCredentials([file(credentialsId: 'kube_config', variable: 'kube_config')]) {
              sh """
                kubectl --kubeconfig $kube_config apply  -f .
                kubectl --kubeconfig $kube_config rollout restart deployment prod-deploy
              """
              }
              
            }
            }
          }
}
}
