pipeline {
    agent any

    environment {
        appVersion = ""
        PATH = "/opt/homebrew/bin:${env.PATH}"
    }

    stages {

        stage('Read version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    env.appVersion = packageJson.version
                    echo "Building version ${env.appVersion}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Image') {
            steps {
                sh "docker build -t catalogue:${env.appVersion} ."
            }
        }
    }
}