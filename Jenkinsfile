import java.text.SimpleDateFormat
def idtag // dataset/analsys id

pipeline {
    agent any

    options {
        timestamps() // Add timestamps to logging
        timeout(time: 2, unit: 'MINUTES') // Abort pipleine

        buildDiscarder(logRotator(numToKeepStr: '8', artifactNumToKeepStr: '8'))
        disableConcurrentBuilds()
    }
    environment {
        PATH = "/usr/local/bin:$PATH"
    }
    parameters {
         string(name: 'idtag', defaultValue: '', description: 'Enter Analysis id')
    }
    

    stages {

        stage('Init') {
            steps {
                echo 'Stage: Init'
                echo "branch=${env.BRANCH_NAME}, params.idtag=${params.idtag}"
                script {
                    if (params.idtag == null || params.idtag == '') {
                        idtag = new SimpleDateFormat("yyyyMMdd_HHmmss").format(new Date())
                    } else {
                        idtag = params.idtag
                    }
                    echo "idtag: ${idtag}"
                }
            }
        }
        
    }
    post {
        always {
            echo "post/always"
            deleteDir() // clean workspace
        }
        success {
            echo "post/success"
        }
        failure {
            echo "post/failure"
        }
    }
}
