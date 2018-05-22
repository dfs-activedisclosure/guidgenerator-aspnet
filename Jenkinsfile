#!/usr/bin/groovy

@Library('github.com/campbelldgunn/jenkins-pipeline@master')
def pipeline = new org.whiteshieldinc.Pipeline()

podTemplate(label: 'jenkins-pipeline', nodeSelector: 'beta.kubernetes.io/os=windows',
    containers: [
        containerTemplate(name: 'jnlp', image: 'campbelldgunn/jnlp-slave-win:latest',
            envVars:[
                containerEnvVar(key: 'HOME', value: 'C:\\users\\containeradministrator'),
                containerEnvVar(key: 'JENKINS_HOME', value: 'C:\\Jenkins')
            ],
            workingDir: 'C:\\Jenkins\\'
        containerTemplate(name: 'docker-windows', image: 'campbelldgunn/docker-windows:v1.0.0', command: 'powershell', ttyEnabled: true),
        containerTemplate(name: 'helm-win', image: 'campbelldgunn/k8s-helm-win:latest')
    ]
)