pipeline {

    agent any

    environment {
        registry = "harmans497"
        registryCredential = 'dockerhub'
    }

    stages {

        stage('Build Client') {
            steps {
                dir('client') {
                    script {
                        sh 'npm install'
                        sh 'npm run build' 
                        dockerImageClient = docker.build registry + "/chat-app-client:V$BUILD_NUMBER"
                        docker.withRegistry('', registryCredential) {
                            dockerImageClient.push("V$BUILD_NUMBER")
                            dockerImageClient.push('latest')
                        }
                    }
                }
            }
        }

        stage('Build Server') {
            steps {
                dir('server') {
                    script {
                        sh 'npm install'
                        dockerImageServer = docker.build registry + "/chat-app-server:V$BUILD_NUMBER"
                        docker.withRegistry('', registryCredential) {
                            dockerImageServer.push("V$BUILD_NUMBER")
                            dockerImageServer.push('latest')
                        }
                    }
                }
            }
        }

        stage('Remove Unused Docker Image') {
            steps {
                script {
                    def imageNameclient = "${registry}/chat-app-client:V${BUILD_NUMBER}"
                    def imageNameserver = "${registry}/chat-app-server:V${BUILD_NUMBER}"
                    sh "docker rmi $imageNameclient"
                    sh "docker rmi $imageNameserver"
                }
            }
        }

        stage('Kubernetes Deploy') {
          agent {label 'KOPS'}
            steps {
               sh "helm upgrade --install --force chat-app helm/chat-app --set image.client.repository=${registry}/chat-app-client:V${BUILD_NUMBER},image.server.repository=${registry}/chat-app-server:V${BUILD_NUMBER} --namespace prod"
                
            }
        }

        // ... Rest of your stages

    }
}
