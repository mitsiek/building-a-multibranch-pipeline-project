pipeline {
    agent any

    environment {
        wrap([$class: 'BuildUser']) {
                                      BUILD_USER_EMAIL="${BUILD_USER_EMAIL}"
        }
                                  }

    stages {
        stage('Build') {
            steps {
                sh 'printenv'
            }
        }
    }
}
