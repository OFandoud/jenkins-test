
pipeline {
    agent {label 'slave-1' }
    stages {
        stage('Build image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'user' ,  passwordVariable: 'pass',)])       {
    		sh """
    		     sudo docker build . -t ofandoud/hello-world:latest
    		     sudo docker login -u ${user} -p ${pass}
    		     sudo docker push ofandoud/hello-world:latest
    		    echo done
    		"""
                }
            }
        }
        stage ('deploy app'){
            steps {
                sh """
                kubectl apply -f prod.yaml
                kubectl rollout restart deployment prod-deploy
                echo done
            """
            }
        }
        }
    }
