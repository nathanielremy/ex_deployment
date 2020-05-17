pipeline {
  agent any

	parameters {
		gitParameter branchFilter: 'origin/(.*)', defaultValue: 'master', name: 'BRANCH', type: 'PT_BRANCH'
	}

  stages {
    stage('Copy artifacts') {
      steps {
        copyArtifacts filter: 'myGo2HWmoms_master', fingerprintArtifacts: true, projectName: 'myGo2HWmoms/master', selector: lastSuccessful()
      }
    }
	stage('Deliver to prod') {
		steps {
             		ansiblePlaybook colorized: true,
                    credentialsId: 'aws',
                    disableHostKeyChecking: true,
                    installation: 'asinble',
                    inventory: 'environments/production/host.ini',
                    playbook: 'playbook.yml'
        }
	}
	}
}
