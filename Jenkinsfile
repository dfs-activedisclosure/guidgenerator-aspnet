def randomUUID = UUID.randomUUID().toString().replace("-", "")
def name = "XbrlTaxonomy"
def podLabel = "${name}-${env.BUILD_NUMBER}"

// constants
def doubleQuote = '"'

podTemplate(label: podLabel, nodeSelector: "beta.kubernetes.io/os=windows",
    containers: [
        containerTemplate(
			name: "jnlp", 
			image: "campbelldgunn/jnlp-slave-win:v1.0.1",
            envVars:[
                containerEnvVar(key: "HOME", value: "C:\\users\\containeradministrator"),
                containerEnvVar(key: "JENKINS_HOME", value: "C:\\Jenkins")
            ],
			alwaysPullImage: false,
            workingDir: "C:\\Jenkins\\"),
        containerTemplate(
			name: "docker-windows", 
			image: "campbelldgunn/docker-windows:v1.0.1", 
			command: "powershell",
			alwaysPullImage: false,
			ttyEnabled: true),
        containerTemplate(
			name: "kubectl-win",
			alwaysPullImage: false,
			image: "campbelldgunn/k8s-kubectl-win:v1.0.1"),
        containerTemplate(
			name: "helm-win",
			alwaysPullImage: false,
			image: "campbelldgunn/k8s-helm-win:latest")
    ]
){
  
  node (podLabel) {
    
    checkout scm
    def pwd = pwd()
	
	def description = sh (
        script: "git log -1 --pretty=format:${doubleQuote}%h - %an, %ad : %s${doubleQuote}",
        returnStdout: true
    ).trim()
	
    currentBuild.description = "${description}"
  
    stage ("Do Something") {
      container("jnlp") {
        sh "echo 'do something'"
      }
	}
  }
}