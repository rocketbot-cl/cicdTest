  pipeline {

    agent any

    stages {

        stage("inPr") {
            steps {
                echo "test in pr"
            }
        }
        stage("beginTests") {
            when {
                expression {
                    env.BRANCH_NAME == "qa"
                }
            }
            steps {
                echo "Test running from pull request 2"
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
