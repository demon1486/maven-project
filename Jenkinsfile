pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
		   stage ('Deploy to stagins') {
				steps {
					build job:'deploy_to_staging'
				}
		   }
	   stage ('Deploy to prod') {
				steps {
					timeout(time:5, unit:'DAYS'){
					input message:'Approve PRODUCTION Deployment?'
					}
					build job:'deploy_to_prod'
				}
		   }    
	}
}
  
