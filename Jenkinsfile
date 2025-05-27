pipeline {
    agent any
    
    environment {
        
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/sivakoppala/10-Tier-MicroService-Appliction.git'
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
                                 sh "docker build -t sivakoppala/adservice:latest ."
                                 sh "docker push sivakoppala/adservice:latest"
								 sh " docker rmi sivakoppala/adservice:latest"
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
                                 sh "docker build -t sivakoppala/cartservice:latest ."
                                 sh "docker push sivakoppala/cartservice:latest"
								 sh " docker rmi sivakoppala/cartservice:latest"
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
                                 sh "docker build -t sivakoppala/checkoutservice:latest ."
                                 sh "docker push sivakoppala/checkoutservice:latest"
								 sh " docker rmi sivakoppala/checkoutservice:latest"
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
                                 sh "docker build -t sivakoppala/currencyservice:latest ."
                                 sh "docker push sivakoppala/currencyservice:latest"
								 sh " docker rmi sivakoppala/currencyservice:latest"
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
                                 sh "docker build -t sivakoppala/emailservice:latest ."
                                 sh "docker push sivakoppala/emailservice:latest"
								 sh " docker rmi sivakoppala/emailservice:latest"
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
                                 sh "docker build -t sivakoppala/frontend:latest ."
                                 sh "docker push sivakoppala/frontend:latest"
								 sh " docker rmi sivakoppala/frontend:latest"
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
                                 sh "docker build -t sivakoppala/loadgenerator:latest ."
                                 sh "docker push sivakoppala/loadgenerator:latest"
								 sh " docker rmi sivakoppala/loadgenerator:latest"
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
                                 sh "docker build -t sivakoppala/paymentservice:latest ."
                                 sh "docker push sivakoppala/paymentservice:latest"
								  sh " docker rmi sivakoppala/paymentservice:latest"
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
                                 sh "docker build -t sivakoppala/productcatalogservice:latest ."
                                 sh "docker push sivakoppala/productcatalogservice:latest"
								 sh " docker rmi sivakoppala/productcatalogservice:latest"
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
                                 sh "docker build -t sivakoppala/recommendationservice:latest ."
                                 sh "docker push sivakoppala/recommendationservice:latest"
								 sh " docker rmi sivakoppala/recommendationservice:latest"
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
                                 sh "docker build -t sivakoppala/shippingservice:latest ."
                                 sh "docker push sivakoppala/shippingservice:latest"
								 sh " docker rmi sivakoppala/shippingservice:latest"
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
