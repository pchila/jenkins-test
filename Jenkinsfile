@Library('keptn-library@5.1')_
def keptn = new sh.keptn.Keptn()


node() {

    def commit_id

    def image_name = "christiankreuzbergerdtx/docker-nodejs-demo"

    def project = "pchila-jenkins-test"
    def service = "hello-service"
    def firststage = "dev"

    stage('Preparation') {
        checkout scm
        sh "git rev-parse --short HEAD > .git/commit-id"                        
        commit_id = readFile('.git/commit-id').trim()
    }

    stage('Initialize Keptn Project') {
        // Initialize the Keptn Project - ensures the Keptn Project is created with the passed shipyard
        keptn.keptnInit project:"${project}", service:"${service}", stage:"${firststage}", monitoring: "dynatrace", shipyard: ".keptn/shipyard.yaml"
    }

    stage('Add files to Keptn Project') {
        // Upload quality gate files
        //keptn.keptnAddResources('keptn/dynatrace/dynatrace.conf.yaml','dynatrace/dynatrace.conf.yaml')
        // Upload SLI and SLO files
        keptn.keptnAddResources('.keptn/dynatrace/sli.yaml','dynatrace/sli.yaml')
        keptn.keptnAddResources('.keptn/slo.yaml','slo.yaml')
    }
}
