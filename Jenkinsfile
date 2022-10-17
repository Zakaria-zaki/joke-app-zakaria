pipeline {
    agent any

    parameters {
        choice(choices: ['Node 17', 'Node 18'], name: 'NODE_VERSIONS')
    }

    environment {
        TOKEN = credentials("herokuID2")
    }

    stages {
        stage('build') {
            steps { 
                // this is for the utilistion of the credentials 
                // sh "token = ${TOKEN}"
                nodejs(nodeJSInstallationName: "${params.NODE_VERSIONS}") {
                    sh 'node -v'
                    sh 'npm install'
                    sh 'npm run build'
                    sh 'npm test '
                }
            }
        }

        stage('deploy') {
            steps {
                script {
                docker.withRegistry('https://registry.hub.docker.com', 'dockerId') {
                    def image = docker.build('zattaoui/joke-app-jenkins')

                    image.push('latest')
                }
            }
            }
        }
    }
}