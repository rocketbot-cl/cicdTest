  pipeline {

    agent any

    stages {

        stage("inPr3") {
            steps {
                echo "test in pr"
                echo "third test in pr cause reasons"
                echo "Testing name"
                echo "${env.BRANCH_NAME}"
                echo "--"
                echo "Change ID"
                echo "${CHANGE_ID}"
                echo "Change URL"
                echo "${CHANGE_URL}"
                echo "Change Title"
                script {
                    def myVariable=${CHANGE_TITLE}
                    echo "${myVariable}"
                }
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
