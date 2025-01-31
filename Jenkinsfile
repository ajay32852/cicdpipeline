pipeline {
    agent any

    tools {
        msbuild 'MSBuild 2022' // Ensure this tool is configured in Jenkins
    }

    stages {
     stage('Checkout') {
            steps {
                // Checkout the code from the repository
                git 'https://github.com/ajay32852/cicdpipeline.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    // Run MSBuild to build the solution
                    // bat 'dotnet restore'
                    // bat 'dotnet build --configuration Release'
                     bat 'msbuild Collegedata.sln /p:Configuration=Release'
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    // Run your tests here, if applicable
                    // For example, if you have a test project, you might run:
                    // bat 'vstest.console.exe YourTestProject.dll'
                    echo 'Running tests...'
                }
            }

        }

         stage('Deploy') {
            steps {
                script {
                    // Define the source and destination paths
                      def sourcePath = 'D:\\Projects\\cicdpipeline\\Collegedata\\bin\\Release\\net8.0\\publish\\*' // Adjust
                      def destinationPath = 'C:\\inetpub\\wwwroot\\doctorbook'

                    // Copy the build output to the destination
                    bat "xcopy /E /I /Y ${sourcePath} ${destinationPath}"
                    echo'Copy and deploy code'
                }
            }
        }



    }

    post {
        success {
            echo 'Build and tests completed successfully!'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}