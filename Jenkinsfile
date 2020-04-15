def my_var
 pipeline {
  agent any
   stages {
    stage('Example') {
        steps {
            script{
                wrap([$class: 'BuildUser']) {
                                      BUILD_USER_EMAIL='${BUILD_USER_EMAIL}'
                                  }
            }
        }
    }

    stage('Example2') {
        steps {
             script{
                echo "$BUILD_USER_EMAIL" 
             }

        }
    }

 }
}
