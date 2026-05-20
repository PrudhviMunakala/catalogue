pipeline {
    agent {
        node {
            label 'roboshop-agent'
        }
    }
    environment {
        appVersion = ""
    }
        stages {
                stage('Read version') {
                    steps {
                        script {
                                // Load the package.json file into a Map
                                def packageJson = readJSON file: 'package.json'
                                
                                // Access specific fields
                                appVersion = packageJson.version
                                
                                echo "Building version ${appVersion}"
                             }
                    }
                }
                stage('Build Image') {
                    steps {
                        sh """
                            docker build -t catalogue:${appVersion} .
                            
                          """
                    }
                }
                stage('test') {
                    steps {
                        echo "test success"
                    }
                }
        
    }
}