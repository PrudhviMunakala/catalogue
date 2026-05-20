pipeline {
    agent {
        node {
            label 'roboshop-agent'
        }
    }
    environment {
        appVersion = ""
        AWS_ACCOUNT_ID = "534409839269"
        region = "us-east-1"
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
                stage('Install dependencies') {
                    steps {
                        sh """
                            npm install
                          """
                    }
                }
                stage('Build Image') {
                    steps {
                        // Use the withAWS block to inject credentials and region
                        withAWS(credentials: 'aws-cred', region: "${region}") {
                            sh """
                            aws ecr get-login-password --region ${region} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com
                                docker build -t ${AWS_ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com/roboshop/catalogue:${appVersion} .
                                docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com/roboshop/catalogue:${appVersion}
                            """
                }
            }
                }
                stage('test') {
                    steps {
                        echo "test success"
                    }
                }
        
    }
}