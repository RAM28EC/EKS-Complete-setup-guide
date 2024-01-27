pipeline {
    agent any
    
    environment {
        
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/RAM28EC/10-MicroService-Appliction.git'
            }
        }
        
        stage('SonarQube') {
            steps {
                
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.projectName=10-Tier -Dsonar.java.binaries=. '''
                }
               
            }
        }
        
        stage('adservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/adservice/') {
                                 sh "docker build -t 28cloud/adservice:latest ."
                                 sh "docker push 28cloud/adservice:latest"
				 sh " docker rmi 28cloud/adservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('cartservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/cartservice/src/') {
                                 sh "docker build -t 28cloud/cartservice:latest ."
                                 sh "docker push 28cloud/cartservice:latest"
				 sh " docker rmi 28cloud/cartservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('checkoutservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/checkoutservice/') {
                                 sh "docker build -t 28cloud/checkoutservice:latest ."
                                 sh "docker push 28cloud/checkoutservice:latest"
				 sh " docker rmi 28cloud/checkoutservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('currencyservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/currencyservice/') {
                                 sh "docker build -t 28cloud/currencyservice:latest ."
                                 sh "docker push 28cloud/currencyservice:latest"
				 sh " docker rmi 28cloud/currencyservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('emailservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/emailservice/') {
                                 sh "docker build -t 28cloud/emailservice:latest ."
                                 sh "docker push 28cloud/emailservice:latest"
				 sh " docker rmi 28cloud/emailservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('frontend') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/frontend/') {
                                 sh "docker build -t 28cloud/frontend:latest ."
                                 sh "docker push 28cloud/frontend:latest"
				 sh " docker rmi 28cloud/frontend:latest"
                        }
                    }
                }
            }
        }
		
		stage('loadgenerator') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/loadgenerator/') {
                                 sh "docker build -t 28cloud/loadgenerator:latest ."
                                 sh "docker push 28cloud/loadgenerator:latest"
				 sh " docker rmi 28cloud/loadgenerator:latest"
                        }
                    }
                }
            }
        }
		
		stage('paymentservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/paymentservice/') {
                                 sh "docker build -t 28cloud/paymentservice:latest ."
                                 sh "docker push 28cloud/paymentservice:latest"
				 sh " docker rmi 28cloud/paymentservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('productcatalogservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/productcatalogservice/') {
                                 sh "docker build -t 28cloud/productcatalogservice:latest ."
                                 sh "docker push 28cloud/productcatalogservice:latest"
				 sh " docker rmi 28cloud/productcatalogservice:latest"
                        }
                    }
                }
            }
        }
		
	   stage('recommendationservice') {
             steps {
                 script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/recommendationservice/') {
                                 sh "docker build -t 28cloud/recommendationservice:latest ."
                                 sh "docker push 28cloud/recommendationservice:latest"
				 sh " docker rmi 28cloud/recommendationservice:latest"
                         }
                    }
                }
            }
         }
		
		stage('shippingservice') {
                  steps {
                   script{
                       withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/shippingservice/') {
                                 sh "docker build -t 28cloud/shippingservice:latest ."
                                 sh "docker push 28cloud/shippingservice:latest"
				 sh " docker rmi 28cloud/shippingservice:latest"
                        }
                    }
                }
            }
        }
        
        
             stage('K8-Deploy') {
               steps {
                 withKubeConfig(caCertificate: '', clusterName: 'my-eks8', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://2BCD568E04EC6456125F85067AFE81B9.gr7.ap-south-1.eks.amazonaws.com') {
                         sh 'kubectl apply -f deployment-service.yml'
                         sh 'kubectl get pods '
                         sh 'kubectl get svc'
                }
            }
         }
        
    }
}
