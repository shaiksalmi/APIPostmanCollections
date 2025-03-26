pipeline {
    agent any
    stages {

        stage('Build') {
            steps {
                echo "Building the war"
            }
        }

        stage("Deploy to QA") {
            steps {
                echo "Deploying to QA"
            }
        }

        

        stage('Pull Docker Images') {
            parallel {
                stage('Pull GoRestAPITest Image') {
                    steps {
                        sh 'docker pull salma4429/gorestapitest:1.0'
                    }
                }
                stage('Pull GoRest Image') {
                    steps {
                        sh 'docker pull salma4429/gorestdatatest:1.0'
                    }
                }
            }
        }

        stage('Prepare Newman Results Directory') {
            steps {
                sh 'mkdir -p $(pwd)/newman' 
            }
        }

        stage('Run API Test Cases in Parallel') {
            parallel {
                stage('Run GoRestAPITest Tests') {
                    steps {
                        sh 'docker run --rm -v $(pwd)/newman:/app/results salma4429/gorestapitest:1.0'
                    }
                }
                stage('Run GoRest Tests') {
                    steps {
                        sh 'docker run --rm -v $(pwd)/newman:/app/results salma4429/gorestdatatest:1.0'
                    }
                }
            }
        }

        stage('Publish HTML Extra Reports') {
            parallel {
                stage('Publish GoRestAPITest Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'gorestapitest.html',
                            reportName: 'GoRest API Test Report',
                            reportTitles: ''
                        ])
                    }
                }
                stage('Publish GoRest Report') {
                    steps {
                        publishHTML([
                            allowMissing: false,
                            alwaysLinkToLastBuild: false,
                            keepAll: true,
                            reportDir: 'newman',
                            reportFiles: 'gorest.html',
                            reportName: 'GoRest Report',
                            reportTitles: ''
                        ])
                    }
                }
            }
        }

        stage("Deploy to PROD") {
            steps {
                echo "Deploying to PROD"
            }
        }
    }
}
