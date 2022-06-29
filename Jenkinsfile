
def manualPath = "./example/Manual_cicdTest.pdf"

pipeline {

    agent any

    stages {

        stage("commitValidation") {
            when {
                expression {
                    env.BRANCH_NAME.contains("PR")
                }
            }
            steps {
                //echo "test in pr"
                //echo "third test pr cause reasons"
                //echo "Testing name"
                //echo "${env.BRANCH_NAME}"
                //echo "--"
                //echo "Change ID"
                //echo "${CHANGE_ID}"
                //echo "Change URL"
                //echo "${CHANGE_URL}"
                //echo "Change Title"
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

        stage("documentator") {
            when {
                expression {
                    env.BRANCH_NAME.contains("PR")
                }
            }
            steps {
                sh "cd ../"
                sh "git clone https://github.com/DaniloToroL/module_documentator.git"
                sh "cd module_documentator"
                sh "sudo apt install python3-pip -y"
                sh "pwd"
                sh "ls"
                sh "pip3 install -r ./requirements.txt"
                sh "python3 documentator -m ../cicdTest"
                sh "cd ../cicdTest"
            }
        }

        stage("fileExistence") {
            when {
                expression {
                    env.BRANCH_NAME.contains("PR")
                }
            }
            steps {
                script {
                    if (!fileExists("./README.md")) {
                        error("README file not found")
                    }
                    if (!fileExists("${manualPath}")) {
                        error("Manual file not found")
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
