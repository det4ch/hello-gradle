@Library('piper-lib@master') _

node {
    stage('Build open source Piper') {
        deleteDir()
        git url:'https://github.com/det4ch/jenkins-library', branch: 'master'
        dockerExecute(script: this,  dockerImage: 'docker.wdf.sap.corp:50000/golang:1.21', dockerOptions: '-u 0') {
                        sh 'GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -o piper . && chmod 777 piper'
        }
        sh "./piper version"
        stash name: 'piper-bin', includes: 'piper'
    }
}

sapPiperPipeline script: this