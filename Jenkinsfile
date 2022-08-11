pipeline {
    agent any
     triggers {
        githubPubat()
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
        stage('Publibat'){
             steps{
               bat 'dotnet publibat WebApplication/WebApplication.csproj --configuration Release --no-restore'
             }
        }
        stage('Deploy'){
             steps{
               bat '''for pid in $(lsof -t -i:9090); do
                       kill -9 $pid
               done'''
               bat 'cd WebApplication/bin/Release/netcoreapp3.1/publibat/'
               bat 'nohup dotnet WebApplication.dll --urls="http://127.0.0.1:9090" --ip="127.0.0.1" --port=9090 --no-restore > /dev/null 2>&1 &'
             }
        }        
    }
}
