pipeline {
    agent any 
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: '7d45d4df-5f8a-49e0-af51-c0f629e77c4b', url: 'https://github.com/ThuyLam999/WEBMVC.git'
            }
        }
        
        stage('Restore packages'){
            steps{
                bat "dotnet restore WEBMVC/WEBMVC.csproj"
            }
        }

        stage('Clean'){
            steps{
                bat "dotnet clean WEBMVC/WEBMVC.csproj"
            }
        }

        stage('Build'){
            steps{
                bat "dotnet build WEBMVC/WEBMVC.csproj --configuration Release"
            }
        }

        stage('Deploy'){
           steps {
               bat "\"${tool 'MSBuild'}\" WEBMVC.sln /p:DeployOnBuild=true /p:DeployDefaultTarget=WebPublish /p:WebPublishMethod=FileSystem /p:SkipInvalidConfigurations=true /t:build /p:Configuration=Release /p:Platform=\"Any CPU\" /p:DeleteExistingFiles=True /p:publishUrl=C:\Users\lamhtpham\Desktop\Kiến thức\WebMVC"
           }
        }

        stage('Cleanup') {
            steps {
                deleteDir()
            }
        }
    }
    post {
        success {
            mail bcc: '', body: 'Thông báo kết quả build', cc: '', from: '', replyTo: '', subject: 'Test Run SUCCESSFUL', to: 'thanhthuyyasou234@gmail.com'
        }  

        failure {
            mail bcc: '', body: 'Thông báo kết quả build', cc: '', from: '', replyTo: '', subject: 'Test Run FAILED', to: 'thanhthuyyasou234@gmail.com'
        }
    }
}
