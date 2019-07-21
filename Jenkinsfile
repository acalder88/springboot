#!/usr/bin/env groovy

node() {
    stage("Setup"){
        checkout scm
    }
    stage("Test") {
        withMaven(maven: 'maven') {
            sh("mvn clean test -U")
        }
    }
    stage("Build") {
        sh(" mvn clean package")
    }
}