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

        // stage('Debug - List Files') {
        //     steps {
        //         dir('mern-docker-demo') {
        //             sh 'ls -la'
        //         }
        //     }
        // }

        // Step to clean the previous build: Do this only if clean build is necessary
        //cleans all the test data/ persistance or lovca databases.
        // stage ('Clean Previous Build'){
        //     steps{
        //         echo "Cleaning up containers, networks, volumes, and images from previous builds"
        //         sh 'docker compose down -v --rmi all || true'
        //     }
        // }      

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