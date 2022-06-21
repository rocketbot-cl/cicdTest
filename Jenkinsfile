  pipeline {

    agent any

    stages {

        stage("beginTests") {
            when {
                expression {
                    env.BRANCH_NAME == "qa"
                }
            }
            steps {
                echo "Test running"
            }
        }
    }
    post {

        success {
            echo "Test success"
        }

        failure {
            echo "Test failed"
        }
    }
}
