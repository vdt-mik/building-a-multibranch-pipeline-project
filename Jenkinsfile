pipeline {
    agent any
    environment {
        // nnnn
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    if (env.setBranch) {
                    sh "echo $setBranch"
                    echo "Branch exist.............///////////////..............................................."
                    } else {
                          if (env.setTag) {
                              sh "echo $setTag"
                              echo "SetTag exist.............///////////////..............................................."
                          } else {
                              echo "FAIIIIIILLLLIILILLILIILLILILILILIILLILILILILILILILI"
                          }
                    }
                }
            }
        }
        stage('PR') {
            when {
                anyOf {
                    changeRequest()
                    branch '**/release-*'
                    branch 'development';
                    branch '**/DO-*'
                }
            }
            steps {
                echo "tests development PRRRRR"
            }
        }
        stage('release') {
            when {
                anyOf {
                    branch '**/release-*';
                    branch 'development'
                }
            }
            steps {
                script {
                    echo "tests release............................................1"
                    def scmVars = checkout scm
                    def branchName = scmVars.GIT_BRANCH
                    sh("printenv")
                }
            }
        }
        stage('Deliver for TAG') {
            when {
                tag '**/v.1.*'
            }
            steps {
                script {
                    checkout scm
                    echo "tests TAG.............................................."
                    def scmVars = checkout scm
                    def branchName = scmVars.GIT_BRANCH
                    sh("printenv")
                }
            }
        }
        stage('Deploy for production') {
            when {
                branch 'production'
            }
            steps {
                echo "tests production"
            }
        }
    }
}
