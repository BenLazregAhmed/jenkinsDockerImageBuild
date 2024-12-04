node {
    def app

    stage('Clone') {
        checkout scm
    }

    stage('Build Image') {
        app = docker.build('web')
    }

    stage('Test Image') {
        app.withRun('-p 80:80') { c ->
            sh 'docker ps'
            sh 'curl localhost'
        }
    }
}
