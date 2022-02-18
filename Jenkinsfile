
pipeline {
    agent {label 'slave-1' }

    stages {
        stage('Build image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'user' ,  passwordVariable: 'pass',)])       {
    		sh """
    		    docker build . -t $docker_repo:v6
    		    docker login -u ${user} -p ${pass}
    		    docker push $docker_repo:v6
    		    echo done
    		"""
                }
            }
        }
        stage ('deploy app'){
            steps {
                sh """
                kubectl apply -f prod.yaml
                echo done
            """
            }
        }
        }
    }
