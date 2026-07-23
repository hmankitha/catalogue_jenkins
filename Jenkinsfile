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

                        def appVersion = packageJson.version
                        echo "Building version ${appVersion}"
                    }
                }
            }
            stage('Check Node') {
                steps {
                    sh '''
                        echo "PATH=$PATH"
                        which node || true
                        which npm || true
                        node -v || true
                        npm -v || true
                    '''
                }
            }
            stage('Install Dependencies') {
                steps {
                    script {
                        sh '''
                            export PATH=/opt/homebrew/bin:$PATH
                            node -v
                            npm -v
                            npm install
                        '''
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