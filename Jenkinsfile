pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'dockercred'
        DOCKERHUB_REPO = 'utsavshah0305/day14-docker-jenkins'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Utsav0701/Day-14-jenkins-dockerfile.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    docker.build(DOCKERHUB_REPO)
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        docker.image(DOCKERHUB_REPO).push()
                    }
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    echo "Deploy Stage"
                    sh 'javac Samole.java'
                    sh 'java Sample'
                }
            }
        }
    }

    post {
        always {
            // cleanWs()
            echo "finish"
        }
    }
}
