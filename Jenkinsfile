pipeline { 
    agent any 

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

        stage('Publish Test Results') { 
            steps { 
                sh 'dotnet publish --configuration Release --output ./publish' 
            } 
        } 

        stage('Archive Artifacts') { 
            steps { 
                archiveArtifacts artifacts: 'publish/**', allowEmptyArchive: true 
            } 
        } 
    } 
}

