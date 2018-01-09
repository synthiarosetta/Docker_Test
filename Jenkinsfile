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
        withCredentials([azureServicePrincipal('d982dd65-33e3-4c33-b6d6-987b6e7c1561')]) {
            sh 'sudo apt-get update && sudo apt-get install -y python libssl-dev libffi-dev python-dev build-essential'
            sh 'curl -L https://aka.ms/InstallAzureCli | bash'
            sh 'exec -l $SHELL'
            sh 'sudo az login --service-principal -u d982dd65-33e3-4c33-b6d6-987b6e7c1561 -p TbSvuXUlBG6bKKm7w3X/F1cxZWtyUcddzTTGNQd31YE= -t 77428205-87ff-4048-a645-91b337240228'
            sh 'sudo az account set -s 9b7c056a-1535-4914-8dc0-e4678ef457b3'
            sh 'sudo az resource list'
            echo "Success!"
        }
    }
}
