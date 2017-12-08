node("docker") {
    docker.withRegistry('<<your-docker-registry>>', '<<synthiarosetta>>') {
    
        git url: "<<your-git-repo-url>>", credentialsId: '<<synthiarosetta>>'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "your-project-name"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
