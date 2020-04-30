pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'myGo2HWmoms', fingerprintArtifacts: true, projectName: 'myGo2HWmoms', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
        ansiblePlaybook credentialsId: 'toobox-vagrant-key', inventory: 'hosts.ini', playbook: 'playbook.yml'
      }
    }
  }
}