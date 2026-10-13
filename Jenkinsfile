
pipeline {
    agent any

    options {
        skipDefaultCheckout(true)
    }

    environment {
        APP_NAME = 'hello-python-nti'
        REPO_URL = 'https://github.com/YOUR_GITHUB_USERNAME/nti-python-jenkins.git'
        HOST_PORT = '5000'
        CONTAINER_PORT = '5000'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    credentialsId: 'jenkins-token',
                    url: "${REPO_URL}"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t "$APP_NAME:$BUILD_NUMBER" .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'docker',
                        usernameVariable: 'DOCKER_USERNAME',
                        passwordVariable: 'DOCKER_PASSWORD'
                    )
                ]) {
                    sh '''
                        set -eu

                        echo "$DOCKER_PASSWORD" |
                            docker login -u "$DOCKER_USERNAME" --password-stdin

                        docker tag "$APP_NAME:$BUILD_NUMBER" \
                            "$DOCKER_USERNAME/$APP_NAME:$BUILD_NUMBER"

                        docker push "$DOCKER_USERNAME/$APP_NAME:$BUILD_NUMBER"

                        docker logout
                    '''
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                    docker rm -f "$APP_NAME" 2>/dev/null || true

                    docker run -d \
                        --name "$APP_NAME" \
                        --restart unless-stopped \
                        -p "$HOST_PORT:$CONTAINER_PORT" \
                        "$DOCKER_USERNAME_PLACEHOLDER/$APP_NAME:$BUILD_NUMBER"
                '''
            }
        }
    }

    post {
        success {
            echo 'Python pipeline completed successfully!'
        }
        failure {
            echo 'Python pipeline failed. Check Console Output.'
        }
    }
}
