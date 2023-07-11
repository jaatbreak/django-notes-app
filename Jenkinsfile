pipeline{
          agent any
          stages{
                  stage('cloning code from scm'){
                    steps{
                        git branch: 'main', url: 'https://github.com/jaatbreak/django-notes-app.git'
                        }
                  }
                  stage('Building the docker image'){
                       steps{
                            sh 'docker build -t my-node-app .'
                            sh 'docker tag  my-node-app:latest amansingh12/my-node-app:$BUILD_TAG'
                        }
                  }
                  stage('docker login & push image'){
                    steps{
                         withCredentials([string(credentialsId: 'dockerhub', variable: 'docker_var')]){
                        sh 'docker login -u amansingh12 -p $docker_var'
	                    sh 'docker push amansingh12/my-node-app:$BUILD_TAG'
                                 
                         }
                    }
                 
                }
                stage("Deployment"){
                    steps{
                        sh 'docker run -dit -p 80:8000 amansingh12/my-node-app:$BUILD_TAG ' 
                    }
                }
       }
}    
