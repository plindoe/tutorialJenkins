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
                sh 'python3 -m pip install -U pytest'
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
        stage('install apache') {

            steps {

                sh 'sudo apt install apache2 -y'

            }

        }

    }

}