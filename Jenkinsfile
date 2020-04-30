pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
        copyArtifacts filter: 'myHugePipe_Ruby', fingerprintArtifacts: true, projectName: 'myHugePipe_Ruby', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
        ansiblePlaybook credentialsId: 'toobox-vagrant-key', inventory: 'hosts.ini', playbook: 'playbook.yml'
      }
    }
  }
}