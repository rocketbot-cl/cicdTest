
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
                sh "git clone https://github.com/DaniloToroL/module_documentator.git"
                sh "sudo apt install python3-pip -y"
                sh "pwd"
                sh "ls"
                sh "cd module_documentator"
                sh "git checkout qa"
                sh "cd ../"
                sh "pip3 install -r ./module_documentator/requirements.txt"
                sh "sudo apt install python3-tk -y"
                sh "python3 ./module_documentator/documentator.py -m ./"
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

        stage ("Merge pull request") {
            steps { 
                withCredentials([usernamePassword(credentialsId: 'c93cdd86-9c16-4ebd-a30f-e174cc4d03c3', usernameVariable: 'ACCESS_TOKEN_USERNAME', passwordVariable: 'ACCESS_TOKEN_PASSWORD',)]) {
                    sh "curl -X PUT -d '{\"commit_title\": \"Merge pull request\"}'  https://github.ibm.com/api/v3/repos/rocketbot-cl/cicdTest/pulls/$CHANGE_ID/merge?access_token=$ACCESS_TOKEN_PASSWORD"
                }
            }
        }

        stage("commit") {
            when {
                expression {
                    env.BRANCH_NAME.contains("PR")
                }
            }
            steps {
                script {

                    sh "cd module_documentator"
                    sh "git add ."
                    sh "git commit -m '${env.CHANGE_TITLE}'"
                    sh "git push origin qa"
                    
                }
            }
        }
    }
    post {

        success {
            echo "Test success"
        }

        failure {
            echo "Test failed"
            sh "rm -r ./*"

        }
    }
}
