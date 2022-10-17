pipeline {
    agent any

    parameters {
        choice(choices: ['Node 17', 'Node 18'], name: 'NODE_VERSIONS')
    }

    stages {
        stage ('build') {
            steps { 
                nodejs(nodeJSInstallationName: '${params.NODE_VERSIONS}') {
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