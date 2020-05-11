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
			when {
				expression {
					params.BRANCH == 'master'
				}
			}
            steps {
                ansiblePlaybook colorized: true,
                    credentialsId: 'b8d91b57-41ae-4cc3-9fb3-e540cb083e9a',
                    disableHostKeyChecking: true,
                    installation: 'asinble',
                    inventory: 'environments/production/host.ini',
                    playbook: 'playbook.yml'
            }
    }
        stage('tests prod') {
        when {
				expression {
					params.BRANCH == 'master'
				}
			}
            steps {
                sh 'docker run -v $HOME/workspace/ex_deployment/environments/production:/etc/newman -t postman/newman run "https://www.getpostman.com/collections/434a10daa020cc392009" -e prodoction.postman_environment.json'
                }
        }

        stage('staging') {
            when {
                expression {
                    params.BRANCH == 'staging'
            }
        }
            steps {
                ansiblePlaybook colorized: true,
                    credentialsId: 'b8d91b57-41ae-4cc3-9fb3-e540cb083e9a',
                    disableHostKeyChecking: true,
                    installation: 'asinble',
                    inventory: 'environments/staging/hosts.ini',
                    playbook: 'playbook.yml'
            }
    }

		stage('Test staging') {
			when {
				expression {
					params.BRANCH == 'staging'
				}
			}
            steps {
                sh 'docker run -v $HOME/workspace/ex_deployment/environments/staging:/etc/newman -t postman/newman run "https://www.getpostman.com/collections/434a10daa020cc392009" -e staging.postman_environment.json'
			}
		}
	}
}
