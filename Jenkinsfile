def randomUUID = UUID.randomUUID().toString().replace("-", "")
def name = "GuidGenerator"
def podLabel = "${name}-${env.BUILD_NUMBER}"

// constants
def doubleQuote = '"'

podTemplate(label: podLabel, nodeSelector: "beta.kubernetes.io/os=windows",
    containers: [
        containerTemplate(
			name: "jnlp", 
			image: "campbelldgunn/jnlp-slave-win:v1.0.2",
            envVars:[
                containerEnvVar(key: "HOME", value: "C:\\users\\containeradministrator"),
                containerEnvVar(key: "JENKINS_HOME", value: "C:\\Jenkins")
            ],
			alwaysPullImage: false,
            workingDir: "C:\\Jenkins\\")
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