  pipeline {

    agent any

    stages {

        stage("inPr2") {
            steps {
                echo "test in pr"
                echo "third test in pr cause reasons"
                echo "sera"
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
