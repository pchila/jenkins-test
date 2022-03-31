node() {

    def commit_id

    def image_name = "christiankreuzbergerdtx/docker-nodejs-demo"

    def project = "jenkins-plugin-test-and-maven-sadness"
    def service = "hello-service"
    def firststage = "dev"

    stage('Preparation') {
        checkout scm
        sh "git rev-parse --short HEAD > .git/commit-id"                        
        commit_id = readFile('.git/commit-id').trim()
    }

    stage('Initialize Keptn Project') {
        // Initialize the Keptn Project - ensures the Keptn Project is created with the passed shipyard
        keptn.keptnInit project:"${project}",
          service:"${service}", stage:"${firststage}",
          shipyard: ".keptn/shipyard.yaml",
          keptn_endpoint: "https://rao42797.cloudautomation.dev.dynatracelabs.com/api",
          keptn_bridge: "https://rao42797.cloudautomation.dev.dynatracelabs.com/bridge"
    }

    stage('Add files to Keptn Project') {
        // Upload quality gate files
        //keptn.keptnAddResources('keptn/dynatrace/dynatrace.conf.yaml','dynatrace/dynatrace.conf.yaml')
        // Upload SLI and SLO files
        keptn.keptnAddResources('.keptn/dynatrace/sli.yaml','dynatrace/sli.yaml')
        keptn.keptnAddResources('.keptn/slo.yaml','slo.yaml')
    }

    stage('Configure monitoring') {
      keptn.keptnConfigureMonitoring monitoring:"dynatrace"
    }
}
