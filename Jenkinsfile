node("docker") {
    docker.withRegistry('<<synthiarosetta/mysecondapp>>', '<<synthiarosetta>>') {
    
        git url: "<<https://github.com/synthiarosetta/Docker_Test>>", credentialsId: '<<synthiarosetta>>'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "synthiarosetta/mysecondapp"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
