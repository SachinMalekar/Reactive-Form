pipeline {
    agent any

    environment {
        NODE_VERSION = '18'   // adjust if you need a different Node.js version
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SachinMalekar/Reactive-Form.git'
            }
        }

        stage('Set up Node') {
            steps {
                // Use NodeJS plugin or install manually
                script {
                    def nodeHome = tool name: "NodeJS_${NODE_VERSION}", type: 'NodeJSInstallation'
                    env.PATH = "${nodeHome}/bin:${env.PATH}"
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                dir('reactive_form') {
                    sh 'npm install'
                }
            }
        }

        stage('Build') {
            steps {
                dir('reactive_form') {
                    sh 'npm run build'
                }
            }
        }

        stage('Test') {
            steps {
                dir('reactive_form') {
                    sh 'npm test'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                dir('reactive_form/dist') {
                    archiveArtifacts artifacts: '**/*', fingerprint: true
                }
            }
        }
    }

    post {
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build failed. Please check logs.'
        }
    }
}
