node {
    def container = docker.image('blackhatch:consul');

    stage 'Mirror'
    container.pull()
    docker.withRegistry('https://docker.dockerhub.com', 'docker-registry-login') {

    stage 'Build' 
        sh 'echo placeholder0'

    stage 'Bake Docker images'

        def build = docker.build("blackhatch/consul:${env.BUILD_TAG}", '.')
        build.push();

        stage 'Test Image'
        build.withRun {petclinic ->
            container.inside() {
                sh 'echo placeholder1'
            }
        }

        stage name: 'Promote Image', concurrency: 1
        build.push('latest');
    }
}
