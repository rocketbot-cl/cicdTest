  pipeline {

    agent any

    stages {

        stage("inPr3") {
            steps {
                echo "test in pr"
                echo "third test pr cause reasons"
                echo "Testing name"
                echo "${env.BRANCH_NAME}"
                echo "--"
                echo "Change ID"
                echo "${CHANGE_ID}"
                echo "Change URL"
                echo "${CHANGE_URL}"
                echo "Change Title"
                script {
                    def commitAccepted = ["[hidden]", "[fix]", "[new]"]
                    def changeTitle = env.CHANGE_TITLE
                    def isAccepted = false
                    for (each in commitAccepted) {
                        if(changeTitle.contains(each)){
                            isAccepted = true
                        }
                    }
                    echo "${isAccepted}"
                    if (!isAccepted){
                        error("Not a valid commit")
                    }
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
