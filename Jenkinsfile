pipeline {
    agent any

    parameters {
        choice(choices: ['Node 17', 'Node 18'], name: 'NODE_VERSIONS')
    }

    environment {
        // TOKEN = credentials("herokuID2")
        tag = "registry.heroku.com/joke-app-jenkins/web"
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

        // stage('deploy') {
        //     steps {
        //         script {
        //         docker.withRegistry('https://registry.hub.docker.com', 'dockerId') {
        //             def image = docker.build('zattaoui/joke-app-jenkins')

        //             image.push('latest')
        //         }
        //     }
        //     }
        // }

        // stage('deploy') {

        //     steps {
        //         script {
        //         def image = docker.build('zattaoui/joke-app-jenkins')

        //         docker.withRegistry('https://registry.hub.docker.com', 'dockerId') {
        //             def dockerImage = image
        //             dockerImage.push('latest')
        //         }

        //         docker.withRegistry('https://registry.heroku.com', 'herokuId') {
        //             sh "docker tag zattaoui/joke-app-jenkins ${tag}:latest"
        //             sh "docker push ${tag}:latest"
        //         }
        //         }
        //     }
        // }

        stage('deploy') {
            steps {
                script {
                docker.withRegistry('https://registry.heroku.com', 'herokuId') {
                    sh "docker buildx build --platform linux/amd64 -t ${tag}:latest -t ${tag}:${BUILD_ID} ."

                    sh "docker push ${tag}:latest"
                }
                }

                withCredentials([usernamePassword(credentialsId: 'herokuId', usernameVariable: 'zattaoui', passwordVariable: 'herokuID2')]) {
                    // sh "echo ${USERNAME}  echo ${PASSWORD} | heroku login"
                    sh "HEROKU_API_KEY=${herokuID2} npx heroku container:release web --app=joke-jenkins"
                }
            }
        }
    }
}