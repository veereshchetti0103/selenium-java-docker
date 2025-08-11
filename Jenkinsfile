pipeline{
    agent any

    stages {
        stage('Build Jar') {
            steps {
                echo 'Building...'
                bat 'mvn clean package -DskipTests'
                echo 'Jar built successfully.'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t=veereshchetti/selenium-docker .'
                echo 'Docker image built successfully.'
            }
        }
        stage('Push Docker Image') {
            environment {
                DOCKER_HUB = credentials('dockerhub-cred')
            }
            steps {
                echo 'Logging in to Docker Hub...'
                bat 'docker login -u ${DOCKER_HUB_USR} -p ${DOCKER_HUB_PSW}'
                echo 'Docker login successful.'

                echo 'Pushing Docker image to registry...'
                bat 'docker push veereshchetti/selenium-docker'
                echo 'Docker image pushed successfully.'
            }
        }

    }
    post {
        always {
            echo 'Cleaning up...'
            bat 'docker rmi veereshchetti/selenium-docker || true'
            echo 'Cleanup completed.'
        }
    }

}