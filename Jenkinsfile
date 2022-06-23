  pipeline {

    agent any

    stages {

        stage("inPr3") {
            steps {
                echo "test in pr"
                echo "third test in pr cause reasons"
                echo "Testing names"
                sh "python3 test.py"
                echo "${env.BRANCH_NAME}"
                echo "--"
                echo "Change ID"
                echo "${CHANGE_ID}"
                echo "Change URL"
                echo "${CHANGE_URL}"
                echo "Change Title"
                echo "${CHANGE_TITLE}"
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
