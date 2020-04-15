def BUILD_USER_EMAIL
pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000 -p 5000:5000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
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
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver for development') {
            when {
                branch 'development'
            }
            steps {
                sh './jenkins/scripts/deliver-for-development.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                sh './jenkins/scripts/deploy-for-production.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
    
    post {
    always {
      deleteDir()
    }
    success {
      script {
        if (env.BRANCH_NAME == 'master') {
          emailext (
            to: 'kmitsie48@gmail.com',
            subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} master is fine",
            body: "The master build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
            attachLog: true,
          )
        } else if (env.BRANCH_NAME == 'development') {
          // also send email to tell people their PR status
          emailext (
            to: BUILD_USER_EMAIL,
            subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} development is fine",
            body: "The development build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
            attachLog: true,
          )
        } else {
          // this is some other branch
	  emailext (
            to: "${env.BUILD_USER_EMAIL}",
            subject: "${env.JOB_NAME} #${env.BUILD_NUMBER} production is fine",
            body: "The production build is happy.\n\nConsole: ${env.BUILD_URL}.\n\n",
            attachLog: true,
          )
        } 
      }
    }     
  }
}
