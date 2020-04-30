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

    stage('Run ansible') {
      steps {
          ansiblePlaybook colorized: true,
            credentialsId: '24ac3217-d46b-4ff7-8a31-88feff14941b',
            disableHostKeyChecking: true,
            installation: 'ansible',
            inventory: '/var/lib/jenkins/workspace/ex_eployment/host.ini',
            playbook: '/var/lib/jenkins/workspace/ex_deployment/playbook.yml'
        
      }
    }
  }
}