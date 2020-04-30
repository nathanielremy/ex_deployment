pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'ex_deployment', fingerprintArtifacts: true, projectName: 'ex_deployment', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
        ansiblePlaybook credentialsId: 'toobox-vagrant-key', inventory: 'hosts.ini', playbook: 'playbook.yml'
      }
    }
  }
}