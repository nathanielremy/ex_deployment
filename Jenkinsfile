 pipeline {
  agent any

  stages {
    stage('Copy artifact') {
      steps {
copyArtifacts filter: 'myGo2HWmoms_master', fingerprintArtifacts: true, projectName: 'myGo2HWmoms/master', selector: lastSuccessful()
      }
    }
    stage('Deliver') {
      steps {
	sh 'scp -o StrictHostKeyChecking=no myGo2HWmoms_master vagrant@10.10.50.2'
        /*ansiblePlaybook credentialsId: 'toobox-vagrant-key', inventory: 'hosts.ini', playbook: 'playbook.yml'*/
      }
    }
  }
}