pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "mern_app"
        SSH_CREDENTIAL_ID = "a3164f52-32cb-4ffd-a15a-e73fdefd5351"
    }
    

    stages{

        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM',
                  branches: [[name: '*/ansible']],
                  userRemoteConfigs: [[url: 'https://github.com/Sainjurohan/mern-docker-demo.git']]
                ])
            }
        }       


        // stage('Checkout/ Cloning Repo') {
        //     steps {
        //         echo "Cloning repository..."
        //         sh '''
        //         rm -rf mern-docker-demo
        //         git clone https://github.com/Sainjurohan/mern-docker-demo.git
        //         '''
        //     }
        // }

        stage('Debug - List Files') {
            steps {
                dir('mern-docker-demo') {
                    sh 'ls -la'
                    sh 'cat Jenkinsfile'
                }
            }
        }

        // Step to clean the previous build: Do this only if clean build is necessary
        //cleans all the test data/ persistance or lovca databases.
        // stage ('Clean Previous Build'){
        //     steps{
        //         echo "Cleaning up containers, networks, volumes, and images from previous builds"
        //         sh 'docker compose down -v --rmi all || true'
        //     }
        // }      

        // stage ('Build Docker Images') {
        //     steps{
        //         echo "Building Docker Images for Backend and Frontend"
        //         sh 'docker compose -f docker-compose.yaml build'
        //     }
        // }

        // stage('Run Containers') {
        //     steps{
        //         echo "Starting the containers using docker compose"
        //         sh 'docker compose -f docker-compose.yaml up -d'
        //     }
        // }

        // stage('Run Ansible') {
        //     steps{
        //         echo "Starting Ansible"
        //         sh 'ssh-keyscan -H 44.244.37.186 >> ~/.ssh/known_hosts'
        //         sh 'ansible-playbook -i ansible/inventory.ini ansible/playbook.yml'
        //     }
        // }

        stage('Run Ansible') {
            steps {
                echo "Running Ansible with SSH agent"       
                sshagent(credentials: ["${env.SSH_CREDENTIAL_ID}"]) {
                    sh '''
                        ssh-keyscan -H 44.244.37.186 >> ~/.ssh/known_hosts
                        ansible-playbook -i ansible/inventory.ini ansible/playbook.yml
                    '''
        }
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