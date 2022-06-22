  pipeline {

    agent any

    stages {

        stage("inPr3") {
            steps {
                echo "test in pr"
                echo "third test in pr cause reasons"
                echo "Testing names"
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
