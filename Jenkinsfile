pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockercred') // Adjust this to your credential ID
        DOCKERHUB_REPO = 'utsavshah0305/day14-docker-jenkins' // Adjust this to your DockerHub repository
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Utsav0701/Day-14-jenkins-dockerfile.git' // Adjust this to your repository URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def image = docker.build("java-app:${env.BUILD_ID}")
                    env.DOCKER_IMAGE = image.id
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        docker.image(env.DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    sh 'docker run -d --name java-app -p 8085:8080 ' + env.DOCKERHUB_REPO + ':latest'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
