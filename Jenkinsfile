node {
    def app

    stage('Clone repository') {
        /* checkout the repository  */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        app = docker.build("releaseworks/hellonode")
    }

    stage('Test image') {
        

        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* push the image with two tags:
         * incremental build number from Jenkins
         *  the 'latest' tag.*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
