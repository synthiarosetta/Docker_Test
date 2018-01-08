node {
    
    stage('Clone repository') {
        /* Clone the GitHub repository to our workspace */
        checkout scm
    }

    stage('Build image') {
        /* Building docker image */
        sh 'sudo docker build -t synthiarosetta/testapp1 .'
        //app = docker.build("synthiarosetta/mysecondapp")
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
        sh 'sudo docker login --username synthiarosetta --password Zara@0112'
        /* Pushing docker image to Docker Hub */
        sh 'sudo docker push synthiarosetta/testapp1'
        /* Removing the docker container */
        sh 'sudo docker rm -f testapp1'
        /* Checking if the container has been removed*/
        sh 'sudo docker ps -a'
    }
    
    stage('Deploy') {
         withCredentials([azureServicePrincipal('48fd2f00-b263-46e2-8e89-13f190f2bf85')]) {
            sh 'az login --service-principal -u d982dd65-33e3-4c33-b6d6-987b6e7c1561 -p TbSvuXUlBG6bKKm7w3X/F1cxZWtyUcddzTTGNQd31YE= -t 77428205-87ff-4048-a645-91b337240228'
            sh 'az account set -s 9b7c056a-1535-4914-8dc0-e4678ef457b3'
            sh 'az resource list'
        }
    }
}
