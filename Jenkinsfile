import java.text.SimpleDateFormat
def idtag // dataset/analsys id

pipeline {
    agent any

    options {
        timestamps() // Add timestamps to logging
        timeout(time: 15, unit: 'HOURS') // Abort pipleine

        buildDiscarder(logRotator(numToKeepStr: '10', artifactNumToKeepStr: '10'))
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
                    date = new Date()
                    sdf = new SimpleDateFormat("yyyyMMdd_HHmmss")
                    idtag = sdf.format(date)
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
