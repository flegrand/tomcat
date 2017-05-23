def PROJECT='tomcat'
def GIT_URL='git@github.com:flegrand/'+PROJECT+'.git'
def REGISTRY_URL='registry.demo.cloudcontrolled.net/demo/'+PROJECT

node {
        git branch: env.BRANCH_NAME, credentialsId: 'jenkins', url: GIT_URL

        stage "Build and Push Docker image"
        withDockerRegistry(registry: [credentialsId: 'jenkins']) {
                withDockerServer(server: [uri: 'unix:///var/run/docker.sock']) {
                        dockerImg = docker.build(REGISTRY_URL+':'+env.BRANCH_NAME+'-build'+env.BUILD_NUMBER,'.')
                        dockerImg.push()
                        dockerImg.push(env.BRANCH_NAME)
                }
        }

        // Launch dependant jobs
        //build job: 'app1/master', wait: false
}