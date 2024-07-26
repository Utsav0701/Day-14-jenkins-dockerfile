pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockercred') // Using the stored credentials ID
        DOCKERHUB_REPO = 'utsavshah0305/day14-docker-jenkins' // Your DockerHub repository name
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/Utsav0701/Day-14-jenkins-dockerfile.git', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def imageName = "${env.DOCKERHUB_REPO}:latest"
                    docker.build(imageName)
                }
            }
        }

        // stage('Push Docker Image') {
        //     steps {
        //         script {
        //             def imageName = "${env.DOCKERHUB_REPO}:latest"
        //             docker.withRegistry('https://index.docker.io/v1/', env.DOCKERHUB_CREDENTIALS) {
        //                 docker.image(imageName).push()
        //             }
        //         }
        //     }
        // }

        // stage('Deploy Container') {
        //     steps {
        //         script {
        //             def imageName = "${env.DOCKERHUB_REPO}:latest"
        //             sh "docker run -d --name hello-world-container ${imageName}"
        //         }
        //     }
        // }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
