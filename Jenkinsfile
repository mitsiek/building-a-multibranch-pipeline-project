pipeline{
	agent any
	stages {
		stage('build'){
			parallel {
			
	            stage('GET_BUILD_USER_DETAILS') 
                  {
		             steps {
                       script {
                                  wrap([$class: 'BuildUser']) {
                                      BUILD_USER_EMAIL="${BUILD_USER_EMAIL}"
                                  }
                              }
	              }
		        }
				stage('Build Master') {
					when {
						branch 'master'
					} 
					steps {    
                       emailext (
                         to: 'kmitsie48@gmail.com',
                         subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} master is fine",
                         body: "The master build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
                         attachLog: true,
                       )
					}
				}
				stage('Build development') {
					when {
						branch 'development'
					} 
					steps {
                       emailext (
                         to: 'iammiteshkokare@gmail.com',
                         subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} development is fine",
                         body: "The development build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
                         attachLog: true,
                       )
					}
				}

				stage('Build Branch') {
					when { 
						not {
							anyOf
							{
								branch 'master';
								branch 'development';
							} 
						}
					} 
					steps {
					script{
                      emailext (
                      to: "$BUILD_USER_EMAIL",
                      subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} Production is fine",
                      body: "The Production build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
                      attachLog: true,
                    )	
                     }					
					}
				}
			}
		}
	}
}
