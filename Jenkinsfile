node {
    def app
    def branchName = "${env.BRANCH_NAME}"
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("angelamukanova/kiii-jenkins1")
    }
    stage('Push image') {
        if ( branchName == dev) {
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.dev}-${env.BUILD_NUMBER}")
                app.push("${env.dev}-latest")
                // signal the orchestrator that there is a new version
            }
        }
    }
}
