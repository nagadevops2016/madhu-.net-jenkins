pipeline {
    agent any
     triggers {
        githubPush()
      }
    stages {
        stage('Restore packages'){
           steps{
               bat 'dotnet restore WebApplication.sln'
            }
         }        
        stage('Clean'){
           steps{
               bat 'dotnet clean WebApplication.sln --configuration Release'
            }
         }
        stage('Build'){
           steps{
               bat 'dotnet build WebApplication.sln --configuration Release --no-restore'
            }
         }
        stage('Test: Unit Test'){
           steps {
                bat 'dotnet test XUnitTestProject/XUnitTestProject.csproj --configuration Release --no-restore'
             }
          }
        stage('Publish'){
             steps{
               bat 'dotnet publish WebApplication/WebApplication.csproj --configuration Release --no-restore'
             }
        }
        stage('Deploy'){
             steps{
               bat 'cd WebApplication/bin/Release/netcoreapp3.1/publish/'
               bat 'nohup dotnet WebApplication.dll --urls="http://127.0.0.1:9090" --ip="127.0.0.1" --port=9090 --no-restore > /dev/null 2>&1 &'
             }
        }        
    }
}
