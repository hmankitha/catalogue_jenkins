pipeline{
    agent any

    environment{
        appVersion = ""
    }
        stages{
            stage('Read version'){
                steps{
                    script{

                        def packageJson = readJSON file: 'package.json'

                        appVersion = packageJson.version
                        echo "Building version ${appVersion}"
                    }
                }
            }
            stage('Install Dependencies'){
                steps{
                    script{
                        sh """
                            npm install
                        """    
                    }
                }
            }
            stage('Build Image'){
                steps{
                    script{
                        sh """
                            docker build -t catalogue:${appVersion}
                        """
                    }
                }
            }
        }
}