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
        stage('clean Project') {
            steps {
                script {
                    sh 'dotnet clean MySimpleCoreProject.csproj' // Replace with your project's build command
                }
            }
        }

        stage('Delete Files (Caution!)') {
            steps {
                sh '''
                    rm -rf bin/Release/net8.0/publish*  # Delete all files in the folder
                '''
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
                        zip zipFile: 'MySimpleCoreProject.zip', archive: false, glob: '**'
                    }
                }
                // Archive the zip file
                archiveArtifacts 'bin/Release/net8.0/publish/MySimpleCoreProject.zip'
            }
        }

        stage('Define SSH Connection') {
            def remoteServer = [
                host: '3.91.233.209',
                user: 'ubuntu',
                credentialsId: 'e54bce0f-3a3e-4ec3-bd2e-aec353a5fbc2'
            ]
        }
        stage('Upload File') {
            sshPut(remote: remoteServer, from: 'bin/Release/net8.0/publish/MySimpleCoreProject.zip', into: '/home/ubuntu/myapp')
        }

    }
}
