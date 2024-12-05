pipeline {
    agent {
        label 'AGENT-1'
    }
    options{
        timeout(time: 10,unit: 'MINUTES')
        disableConcurrentBuilds ()
        // retry (1)
    }
     environment {
        DEBUG = 'true'
    }
    stages {
        stage('Read the version') {
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo "App version: ${appVersion}"
                }
            }
        }
        stage('Test') { 
            steps {
                sh 'echo this is test'
                sh 'env'
            }
        }
        stage('Deploy') {
            when {
                expression { env.GIT_BRANCH != "origin/main" }
            }
            steps {

                    sh 'echo This is deploy'
                    //error 'pipeline failed'

            }
        }
        stage('print params'){
            steps{
                echo "Hello ${params.PERSON}"
                echo "Biography: ${params.BIOGRAPHY}"
                echo "Toggle: ${params.TOGGLE}"
                echo "Choice: ${params.CHOICE}"
                echo "Password: ${params.PASSWORD}"

            }
        }
    //       stage('Approval'){
    //          input {
    //              message "Should we continue?"
    //             ok "Yes, we should."
    //             submitter "alice,bob"
    //              parameters {
    //                 string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //              }
    //          }
    //         steps {
    //             echo "Hello, ${PERSON}, nice to meet you."
    //         }
    //  }
    }

post {
    always{
        echo 'This sections runs always'
        deleteDir() 
    }
    success{
        echo 'This section runs when pipeline success'
    }
    failure{
        echo 'This section runs when pipline failure'
    }
    }
}


