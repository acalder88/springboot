#!/usr/bin/env groovy

node() {
    stage("Setup"){
        checkout scm
    }
    stage("Test") {
        sh("mvn clean test -U")
    }
    stage("Build") {
        sh(" mvn clean package")
    }
}