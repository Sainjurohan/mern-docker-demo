pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "mern_app"
    }

    stages{
        stage('Checkout/ Cloning Repo') {
            steps {
                echo "Cloning repository..."
                sh 'git clone https://github.com/Pravesh-Sudha/MERN-docker-compose.git
'
            }
        }

        stage ('Build Docker Images') {
            steps{
                echo "Building Docker Images for Backend and Frontend"
                sh 'docker-compose -f docker-compose.yml build'
            }
        }

        stage('Run Containers') {
            steps{
                echo "Starting the containers using docker compose"
                sh 'docker-compose -f docker-compose.yml up -d'
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