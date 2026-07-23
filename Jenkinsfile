pipeline{
    agent any

    environment{
        appVersion = ""
    }
        stages{
            stage('Read version'){
                steps{
                    script{

                        def package = readJSON file: 'package.json'

                        env.appVersion = packageJson.version
                        echo "Building ${appName} version ${appVersion}"
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