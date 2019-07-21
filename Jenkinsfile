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
            withMaven(maven: 'maven', jdk: 'jdk') {
                sh(" mvn clean package")
            }
        }
    } catch(error) {
        throw error
    } finally {
        cleanWs()
    }
}