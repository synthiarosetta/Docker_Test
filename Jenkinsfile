import groovy.json.JsonSlurper
node {

    def container
    def acrSettings
    
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
        sh 'sudo docker rm -f testapp1'
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
    
    stage('Push image to AKS'){
        echo "Pushing image to AKS"
        stage('Deploy') {
        withCredentials([azureServicePrincipal('principal-credentials-id')]) {
            sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
            sh 'az account set -s $AZURE_SUBSCRIPTION_ID'
            sh 'az resource list'
        }
      }
    }
}
