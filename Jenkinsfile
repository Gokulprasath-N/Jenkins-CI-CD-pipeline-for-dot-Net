pipeline {
    agent any  // Use any available Jenkins agent

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', // Replace with your branch name
                    credentialsId: '532e9f8c-e06b-4621-8df1-5357609c9628', // Replace with your credential ID
                    url: 'https://github.com/Gokulprasath-N/simple_asp.net_project.git' // Replace with your GitHub URL
            }
        }
        stage('Build Project') {
            steps {
                script {
                    // Use the appropriate .NET command for your project (e.g., dotnet build, msbuild)
                    sh 'dotnet build MySimpleCoreProject.csproj' // Replace with your project's build command
                }
            }
        }
        // Add additional stages for testing (optional)
        /*
        stage('Run Tests') {
            steps {
                // Use the appropriate test runner for your project (e.g., dotnet test, xunit)
                sh 'dotnet test MyProject.Tests --no-build' // Replace with your test command
            }
        }
        */

        stage('Publish Project') {
            steps {
                script {
                    // Use the appropriate .NET command for your project (e.g., dotnet build, msbuild)
                    sh 'dotnet publish MySimpleCoreProject.csproj' // Replace with your project's build command
                }
            }
        }
        
       stage('Zip and Archive Artifacts') {
            steps {
                script {
                    // Create a zip archive of the desired folder
                    dir('bin/Release/net8.0/publish') { // Replace with actual path
                        zip zipFile: 'MySimpleCoreProject.zip', archive: false, glob: 'bin/Release/net8.0/publish/**'
                    }
                }
                // Archive the zip file
                archiveArtifacts 'MySimpleCoreProject.zip'
            }
        }
    }
}
