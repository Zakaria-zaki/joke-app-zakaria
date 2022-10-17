pipeline {
    agent any

    parameters {
        choice(choices: ['node 17', 'node 18', 'node 19'], name: 'NODE_VERSIONS')
    }

    stages {
        stage ('build') {
            steps { 
                nodejs(nodeJSInstallationName: ${params.NODE_VERSIONS}) {
                    sh 'npm -v'
                    sh 'npm i -g pnpm'
                    sh 'pnpm install --frozen-lockfile'
                    sh 'pnpm build'
                    sh 'pnpm test '
                }
            }
        }
    }
}