pipeline {
    agent any
    environment {
        // nnnn
        CI = 'true'
    }
    stages {
        stage('Build') {
            when {
                anyOf {
                    expression { setBranch != null }
                }
            }
            steps {
                sh "echo $setBranch"
                echo "Branch exist.............///////////////..............................................."
            }
        }
        stage('Test') {
            when {
                anyOf {
                    expression { setTag != null }
                }
            }
            steps {
                sh "echo $setTag"
                echo "SetTag exist.............///////////////..............................................."
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
