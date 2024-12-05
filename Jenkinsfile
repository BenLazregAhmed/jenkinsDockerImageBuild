node {
    def app

    stage('Clone') {
        checkout scm
    }

    stage('Build Image') {
        app = docker.build("ahmedevops/web:${env.BUILD_ID}")
    }

    stage('Test Image') {
        app.withRun('-p 8080:80') { c ->
            sh 'docker ps'
            sh 'curl localhost:8080'
        }
    }

    stage('Push Image') {
        docker.withRegistry('https://index.docker.io/v1/', 'docker-hub1') {
            app.push() // Push the versioned tag
            app.push('latest') // Push a 'latest' tag for easier reference
        }
    }
}
