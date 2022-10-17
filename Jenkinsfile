pipeline {
    agent any

    stages {
        stage ('build') {
            steps { 
                nodejs(nodeJSInstallationName: 'Node 17') {
                    sh 'npm -v'
                    sh 'npm i -g pnpm'
                    sh 'pnpm install --frozen-lockfile'
                    sh 'pnpm build'
                    sh 'pnpm test'
                }
            }
        }
    }
}