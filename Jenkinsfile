pipeline {
    agent any

    stages {
        stage("Restore Dependencies") {
            steps {
                echo 'Restoring Dependencies..'
                bat 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
                bat 'dotnet build'
            }
        }
        stage('Test') {
            parallel {
                stage('TestProject1 Tests') {
                    steps {
                        echo 'Running TestProject1 Tests..'
                        bat 'dotnet test TestProject2/TestProject2.csproj --logger trx;LogFileName=TestResults.trx'
                    }
                }
                stage('TestProject2 Tests') {
                    steps {
                        echo 'Running TestProject2 Tests..'
                        bat 'dotnet test TestProject2/TestProject2.csproj --logger trx;LogFileName=TestResults.trx'
                    }
                }
                stage('TestProject3 Tests') {
                    steps {
                        echo 'Running TestProject3 Tests..'
                        bat 'dotnet test TestProject3/TestProject3.csproj --logger trx;LogFileName=TestResults.trx'
                    }
                }
            }
        }
        
    }

    post {
        always {
            archiveArtifacts '**/TestResults/*.trx'
            publishChecks name: 'Jenkins Build'  
        }
    }
}
