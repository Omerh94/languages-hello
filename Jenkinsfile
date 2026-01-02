pipeline {
    agent any

    parameters {
        choice(
            name: 'LANG',
            choices: ['JAVA', 'PYTHON', 'C', 'ALL'],
            description: 'Choose which file to print'
        )
    }

    stages {
        stage('Show selection') {
            steps {
                echo "Selected option: ${params.LANG}"
            }
        }

        stage('Print content') {
            steps {
                script {
                    if (params.LANG == 'ALL') {
                        sh 'echo "----- JAVA -----"; cat JAVA'
                        sh 'echo "----- PYTHON -----"; cat PYTHON'
                        sh 'echo "----- C -----"; cat C'
                    } else {
                        sh "echo \"----- ${params.LANG} -----\""
                        sh "cat ${params.LANG}"
                    }
                }
            }
        }
    }

    post {
        always {
            mail to: 'omerhorovitz1@gmail.com',
                 subject: "Jenkins result - Selected: ${params.LANG}",
                 body: "Pipeline finished.\nSelected language: ${params.LANG}\nJob: ${env.JOB_NAME}\nBuild: #${env.BUILD_NUMBER}\nURL: ${env.BUILD_URL}"
        }
    }
}
