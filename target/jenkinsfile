#!/user/bin/env groovy

node('master') {
    try {
        stage('Checkout'){
            checkout scm
        }

        stage('Build'){
            bat 'nuget.exe restore HelloWorld.sln'
            bat "\"${tool 'MSBuild-15.0'}\" HelloWorld.sln /p:Configuration=Release /p:Platform=\"Any CPU\" /p:ProductVersion=1.0.0.${env.BUILD_NUMBER}"
        }

        stage('Archive'){
            archive '*'
        }
    }
    catch(error){
        throw error
    }
    finally{

    }
}