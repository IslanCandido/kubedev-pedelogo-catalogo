pipeline {
    agent any

    stages {
        stage('Get Source') {
            steps {
                git url: 'https://github.com/IslanCandido/kubedev-pedelogo-catalogo.git',
                branch: 'master'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerapp = docker.build("islandev/pedelogo-catalogo:${env.BUILD_ID}",
                    '-f ./src/PedeLogo.Catalogo.Api/Dockerfile')
                }
            }
        }

        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.push("latest")
                    dockerapp.push("${env.BUILD_ID}")
                }
            }
        }
    }
}