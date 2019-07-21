#!/usr/bin/env groovy

node() {
    try{
        stage("Setup"){
            checkout scm
        }
        stage("Test") {
            withMaven(maven: 'maven', jdk: 'jdk') {
                sh("mvn clean test -U")
            }
        }
        stage("Build") {
            sh(" mvn clean package")
        }
    } catch(error) {
        sendFailureEmail(committerEmail)
        throw error
    } finally {
        cleanWs()
    }
}