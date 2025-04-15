pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "mern_app"
    }

    stages{
        stage('Checkout/ Cloning Repo') {
            steps {
                echo "Cloning repository..."
                sh '''
                rm -rf mern-docker-demo
                git clone https://github.com/Sainjurohan/mern-docker-demo.git
                '''
            }
        }

        stage ('Build Docker Images') {
            steps{
                echo "Building Docker Images for Backend and Frontend"
                sh 'docker compose -f docker-compose.yaml build'
            }
        }

        stage('Run Containers') {
            steps{
                echo "Starting the containers using docker compose"
                sh 'docker compose -f docker-compose.yaml up -d'
            }
        }
    }

    post{
        always {
            echo "Pipeline Finished"
        }
        failure {
            echo "Something went wrong during the pipeline"
        }
    }
}