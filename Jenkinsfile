 pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
copyArtifacts filter: 'myGo2HWmoms_master', fingerprintArtifacts: true, projectName: 'myGo2HWmoms/master', selector: lastSuccessful()
      }
    }


stage('Run ansible') {
      steps {
          ansiblePlaybook colorized: true,
            credentialsId: '24ac3217-d46b-4ff7-8a31-88feff14941b',
            disableHostKeyChecking: true,
            installation: 'asinble',
            inventory: '/var/lib/jenkins/workspace/ex_deployment/host.ini',
            playbook: '/var/lib/jenkins/workspace/ex_deployment/playbook.yml'
      }
    }
}