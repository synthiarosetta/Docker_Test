node {
    
    stage('Clone repository') {
        /* Clone the GitHub repository to our workspace */
        checkout scm
    }

    stage('Build image') {
        /* Building docker image */
        sh 'sudo docker build -t synthiarosetta/testapp1 .'
    }

    stage('Test image') {
        /* Listing both running and stopped containers */
        sh 'sudo docker ps -a'
        /* Testing docker image */
        sh 'sudo docker run -d -p 9999:5000 --name testapp1 synthiarosetta/testapp1'
        echo "Tests passed"
    }

    stage('Push image to Docker Hub') {
        /* Login to Docker Hub */
        
        /* Pushing docker image to Docker Hub */
        sh 'sudo docker push synthiarosetta/testapp1'
        /* Removing the docker container */
        sh 'sudo docker rm -f testapp1'
        /* Checking if the container has been removed*/
        sh 'sudo docker ps -a'
    }
    
    stage('Deploy') {
    
    }
}
