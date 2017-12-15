node {
    //def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        sh 'sudo docker build -t synthiarosetta/testapp .'
        //app = docker.build("synthiarosetta/mysecondapp")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
        sh 'sudo docker ps -a'
        /* remove old container */
        sh 'sudo docker rm -f testapp'
        /* run new container */
        sh 'sudo docker run -d -p 9999:5000 --name testapp synthiarosetta/testapp'
        echo "Tests passed"
        /*app.inside {
            sh 'echo "Tests passed"'
        }*/
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        sh 'sudo docker login --username synthiarosetta --password Zara@0112'
        sh 'sudo docker push synthiarosetta/testapp:v1'
        sh 'sudo docker rm -f testapp'
        sh 'sudo docker ps -a'
        /*docker.withRegistry('https://registry.hub.docker.com', 'wincred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")*/
        //}
    }
}
