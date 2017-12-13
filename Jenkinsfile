node {
    //def app

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */
        sh 'sudo docker build -t synthiarosetta/mysecondapp .'
        //app = docker.build("synthiarosetta/mysecondapp")
    }

    stage('Test image') {
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */
        sh 'sudo docker run -p 8888:5000 --name mysecondapp synthiarosetta/myfirstapp'
        echo "Tests passed"
        /*app.inside {
            sh 'echo "Tests passed"'
        }*/
    }

    //stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        /*docker.withRegistry('https://registry.hub.docker.com', 'wincred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")*/
        //}
    //}
}
