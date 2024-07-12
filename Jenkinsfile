pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/dotnetwebapp" // Adjust this to your desired deployment directory
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/adeelshafi79/dotnetwebapp.git', branch: 'master'
            }
        }

        stage('Restore') {
            steps {
                sh 'pwd'
                sh 'dotnet restore'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build --configuration Release'
            }
        }

        stage('Test') {
            steps {
                sh 'pwd'
                sh 'dotnet test --no-build --verbosity normal'
            }
        }

        stage('Publish') {
            steps {
                sh 'dotnet publish --configuration Release --output ./publish'
                sh "sudo cp -r ./publish/* ${DEPLOY_DIR}"
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'publish/**', allowEmptyArchive: true
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Stop the running application (if any)
                    sh 'sudo systemctl stop dotnetwebapp'

                    

                    // Start the application
                    sh 'sudo systemctl start dotnetwebapp'
                }
            }
        }
    }
}

