def my_var
pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                my_var = 'value1'
            }
        }

        stage('Example2') {
            steps {
                printl(my_var)
            }
        }

    }
}
