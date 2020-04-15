pipeline {
    agent any

    environment {
        script {
                                  wrap([$class: 'BuildUser']) {
                                      BUILD_USER_EMAIL=${BUILD_USER_EMAIL}
                                  }
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
