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
        mail body: "project build error is here: ${env.BUILD_URL}", 
                        subject: 'pipeline test email: fail', 
                        to: 'cxu@acr.org'
        throw error
    }
    finally{
        mail body: 'project build successful', 
                        subject: 'pipeline test email: successful', 
                        to: 'cxu@acr.org'
    }
}