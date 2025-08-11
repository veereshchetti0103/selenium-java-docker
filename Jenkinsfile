pipeline{
    agent docker {
        image 'maven:3.9.4-eclipse-temurin-21'
        args '-v /var/run/docker.sock:/var/run/docker.sock'
    }

    stages {
        stage('Build Jar') {
            steps {
                echo 'Building...'
                sh 'mvn clean package -DskipTests'
                echo 'Jar built successfully.'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t=veereshchetti/selenium-docker .'
                echo 'Docker image built successfully.'
            }
        }
        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to registry...'
                sh 'docker push veereshchetti/selenium-docker'
                echo 'Docker image pushed successfully.'
            }
        }

    }


}