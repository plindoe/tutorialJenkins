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
        stage('install apache') {

            steps {

                sh 'sudo apt install apache2 -y'

            }

        }

    }

}