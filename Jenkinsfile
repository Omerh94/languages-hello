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
            echo "=== EMAIL SIMULATION ==="
            echo "To: your@email.com"
            echo "Subject: Jenkins result for ${params.LANG}"
            echo "Body: Selected language = ${params.LANG}, Build = ${env.BUILD_NUMBER}, Status = ${currentBuild.currentResult}"
            echo "========================"
        }
    }
}
