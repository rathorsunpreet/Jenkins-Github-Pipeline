// OS is 1 for Windows and 0 for Linux or Mac
def OS = 1
// Default value for user input
def userInput = "all report"
pipeline {
    agent any

    tools {
        git "git"
        nodejs "node-22.2.0"
    }

    stages {
        stage('CheckOS') {
            steps {
                script {
                    if (isUnix()) {
                        OS = 0
                    }
                    // Else it remains 1
                }
            }
        }
        stage('Init') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/rathorsunpreet/SimpleAPITestInterface.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    if (OS == 1) {
                        bat("npm install")
                    } else {
                        sh("npm install")
                    }
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    try {
                        timeout(time: 1, unit: 'MINUTES') {
                            userInput = input(
                                id: 'userInput', message: 'Enter API names',
                                parameters: [
                                    [$class: 'StringParameterDefinition',
                                      defaultValue: 'all report',
                                      description: '',
                                      name: 'apiFiles'
                                    ]
                                ]
                            )
                        }
                    } catch (err) {
                        CauseOfInterruption card = err.getCauses()[0]
                        if (card.toString().contains('ExceededTimeout') == true) {
                            echo ('System Timeout!')
                        } else {
                            echo ('User Aborted!')
                            currentBuild.result = 'ABORTED'
                            error('Aborting the build.')
                        }
                    }
                    if (OS == 1) {
                        bat("npm run test " + userInput)
                    } else {
                        sh("npm run test " + userInput)
                    }
                }
            }
        }
        stage('Archive') {
            when {
                beforeAgent true
                expression {
                    return userInput.contains('report')
                }
            }
            steps {
                script {
                    echo (env.WORKSPACE)
                    def dirPath = 'HTML_Report'
                    zip zipFile: 'HTML_Report.zip', archive: true, dir: dirPath, overwrite: true, glob: ''
                }
            }
        }
    }
}
