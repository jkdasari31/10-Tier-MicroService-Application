pipeline {
    agent any

    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/jkdasari31/10-Tier-MicroService-Application.git'
            }
        }
        stage('Static Code Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.projectName=10-Tier -Dsonar.java.binaries=. '''
                }
            }
        }
        stage('adservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/adservice/'){
							sh "docker build -t jkdasari/adservice:latest ."
							sh "docker push jkdasari/adservice:latest"
							sh "docker rmi jkdasari/adservice:latest"
						}
					}
				}
            }
        }
        stage('cartservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/cartservice/src/'){
							sh "docker build -t jkdasari/cartservice:latest ."
							sh "docker push jkdasari/cartservice:latest"
							sh "docker rmi jkdasari/cartservice:latest"
						}
					}
				}
            }
        }
        stage('checkoutservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/checkoutservice/'){
							sh "docker build -t jkdasari/checkoutservice:latest ."
							sh "docker push jkdasari/checkoutservice:latest"
							sh "docker rmi jkdasari/checkoutservice:latest"
						}
					}
				}
            }
        }
        stage('emailservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/emailservice/'){
							sh "docker build -t jkdasari/emailservice:latest ."
							sh "docker push jkdasari/emailservice:latest"
							sh "docker rmi jkdasari/emailservice:latest"
						}
					}
				}
            }
        }
        stage('frontend') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/frontend/'){
							sh "docker build -t jkdasari/frontend:latest ."
							sh "docker push jkdasari/frontend:latest"
							sh "docker rmi jkdasari/frontend:latest"
						}
					}
				}
            }
        }
        stage('loadgenerator') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/loadgenerator/'){
							sh "docker build -t jkdasari/loadgenerator:latest ."
							sh "docker push jkdasari/loadgenerator:latest"
							sh "docker rmi jkdasari/loadgenerator:latest"
						}
					}
				}
            }
        }
        stage('paymentservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/paymentservice/'){
							sh "docker build -t jkdasari/paymentservice:latest ."
							sh "docker push jkdasari/paymentservice:latest"
							sh "docker rmi jkdasari/paymentservice:latest"
						}
					}
				}
            }
        }
        stage('productcatalogservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/productcatalogservice/'){
							sh "docker build -t jkdasari/productcatalogservice:latest ."
							sh "docker push jkdasari/productcatalogservice:latest"
							sh "docker rmi jkdasari/productcatalogservice:latest"
						}
					}
				}
            }
        }
        stage('recommendationservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/recommendationservice/'){
							sh "docker build -t jkdasari/recommendationservice:latest ."
							sh "docker push jkdasari/recommendationservice:latest"
							sh "docker rmi jkdasari/recommendationservice:latest"
						}
					}
				}
            }
        }
        stage('shippingservice') {
            steps {
                script{
					withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){
						dir('/var/lib/jenkins/workspace/10-Tier/src/shippingservice/'){
							sh "docker build -t jkdasari/shippingservice:latest ."
							sh "docker push jkdasari/shippingservice:latest"
							sh "docker rmi jkdasari/shippingservice:latest"
						}
					}
				}
            }
        }
        stage('Deploy app to k8s') {
            steps {		
				withKubeConfig(caCertificate: '', clusterName: 'my-eks2', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://61DE1E3F03223FADADAD2881CDD42841.gr7.ap-south-1.eks.amazonaws.com') {
					sh 'kubectl apply -f deployment-service.yml'
                    sh 'kubectl get pods'
                    sh 'kubectl get svc'
				}
			}
		}
        
    }
}