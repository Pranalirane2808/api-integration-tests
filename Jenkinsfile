pipeline {
    agent any

    environment {
        COLLECTION = 'collection.json'
        ENV = 'environment.json'
    }

    stages {
        stage('Install Newman') {
            steps {
                sh 'npm install -g newman'
            }
        }

        stage('Run Postman Tests') {
            steps {
                sh "newman run ${COLLECTION} -e ${ENV} --reporters cli,junit --reporter-junit-export results.xml"
            }
        }

        stage('Publish Test Results') {
            steps {
                junit 'results.xml'
            }
        }
    }

    post {
        always {
            echo 'Build complete.'
        }
    }
}
