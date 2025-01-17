pipeline {

    agent any

    parameters {

        booleanParam(name: 'Refresh',

                    defaultValue: false,

                    description: 'Read Jenkinsfile and exit.')

            }

    stages {

        stage('update apt cache') {

            steps {

                sh 'sudo apt update'

            }

        }

        stage('Clean Up') {
            steps {
                sh 'sudo docker system prune -a -f'
            }
            }
        stage('Build') {
            steps {
                sh 'sudo docker-compose build'
            }
        }
        stage('Install Dependacies') {
            steps {
                sh '''
                      sudo apt install python3-pip -y
                      python3 -m pip install -U pytest
                      python3 -m pip install -U flask
                      python3 -m pip install -U flask_testing
                      python3 -m pip install -U requests
                      pip install requests_mock
                      
                   '''
            }
        }
        stage('Unit Tests') {
            steps {
                sh '''
                      python3 -m pytest ./converter/tests/test_unit.py
                      python3 -m pytest ./prime/tests/test_unit.py
                   '''
            }
        }
        stage('Integration Test') {
            steps {
                sh 'python3 -m pytest ./main/tests/test_unit.py'
            }
        }
        // stage('Deploying') {
        //     steps {
        //         sh '''
        //             ssh -i /home/jenkins/.ssh/Estio-Training-NForester -o StrictHostKeyChecking=no jenkins@10.0.1.10
        //             sudo docker-compose -f /home/ubuntu/APIPrimeAge/docker-compose.yaml down
        //             sudo docker system prune -a -f                  
        //             sudo docker-compose -f /home/ubuntu/APIPrimeAge/docker-compose.yaml build
        //         '''
        //     }
        // }
         //172.31.37.211
        stage('Remote install') {
            steps {
                sh '''
                      #!/bin/bash
                      ssh -i /home/jenkins/.ssh/New-Key -o StrictHostKeyChecking=no ubuntu@18.130.112.76 << EOF
                      sudo apt-get update                      
                      sudo apt-get install docker -y
                      sudo apt-get install docker-compose -y
                      git clone https://github.com/plindoe/tutorialJenkins
                      cd tutorialJenkins
                      sudo docker-compose down
                      sudo docker system prune -a -f
                      sudo docker-compose up --build -d
                      exit 0
                      << EOF
                   '''
            }
        }
        stage('install apache') {

            steps {

                sh 'sudo apt install apache2 -y'

            }

        }

    }

}