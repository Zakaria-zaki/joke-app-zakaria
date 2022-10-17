pipeline {
    agent any

    parameters {
        choice(choices: ['node 17', 'node 18', 'node 19'], name: 'NODE_VERSIONS')
    }

    stages {
        stage ('build') {
            steps { 
                nodejs(nodeJSInstallationName: '${params.NODE_VERSIONS}') {
                    sh 'npm -v'
                    sh 'npm install'
                    sh 'npm build'
                    sh 'npm test '
                }
            }
        }
    }
}