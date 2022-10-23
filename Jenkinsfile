pipleline{
    agent any

    stages{
        stage('Build Docker Image'){
            steps{
                script{
                    dockerapp = docker.build("estulano/kube-news:${env.BUILD_ID}", 'src/Dockerfile src')
                }
            }
        }

        stage ('Push Docker Image'){
            steps{
                script{
                    docker.withDockerRegistry('https://registry.hub.docker','dockerhub')
                    dockerapp.push('v1')
                    dockerapp.push(${env.BUILD_ID})
                }
            }
        }

        stage('Deploy Kubernetes'){
            steps{
                withKubeConfig([credentialsId: 'kubeconfig']){
                    ssh 'kubectl apply -f src/deployment.yaml'
                }
            }
        }
    }

}