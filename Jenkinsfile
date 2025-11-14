pipeline{
    agent any
    tools{
        maven "maven"
    }
    stages{
        stage("SCM checkout"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/nilanghosh77/jenkins-ci-cd.git']])
            }
        }
        stage("Maven build process"){
            steps{
                script{
                    sh 'mvn clean install'
                }
            }
        }

    }
    post{
        always{
            emailext attachLog: true, body: '''<html>
    <body>
       <p> Build Number : ${BUILD_NUMBER} </p>
       <p> Build Status : ${BUILD_STATUS} </p>
       <p> Check the  <a href="${BUILD_URL}" > Console output </a> </p>
    </body>
</html>''', mimeType: 'text/html', replyTo: 'nilanghosh77@gmail.com', subject: 'Pipeline Status: ${BUILD_NUMBER}', to: 'nilanghosh77@gmail.com'
        }
    }
}