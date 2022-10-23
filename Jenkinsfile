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
    }

}