#!/usr/bin/env groovy

def buildDockerImage(version, snapshot) {
    def host = "629546332162.dkr.ecr.us-east-1.amazonaws.com"
    def repo = "springboot"
    def region = "us-east-1"
    def tag = "${version}-${snapshot}"
    def endpoint = "${host}/${repo}:${tag}"
    echo("Building docker image: ${endpoint}")
    sh("\$(aws ecr get-login --no-include-email  --region ${region})")
    sh("docker build . -t ${endpoint}")
    def image =  [
        version: "${version}",
        snapshot:"${snapshot}",
        repo: "${repo}",
        host:"${host}",
        endpoint:"${endpoint}",
        tag:"${tag}"
    ]
    return image
}

def copyJar() {
    sh("cp target/demoBack*.jar docker/demoBack.jar")
}

def getVersion() {
    return sh(script:"mvn -q -Dexec.executable=echo -Dexec.args='\${project.version}' --non-recursive exec:exec | tail -1", returnStdout: true)
}



node() {
    def version
    try{
        stage("Setup"){
            checkout scm
            withMaven(maven: 'maven', jdk: 'jdk') {
                version = getVersion()
            }
            echo ("${version}")
        }
        stage("Test") {
            withMaven(maven: 'maven', jdk: 'jdk') {
                sh("mvn clean test -U")
            }
        }
        stage("Build") {
            withMaven(maven: 'maven', jdk: 'jdk') {
                sh(" mvn clean package -DskipTests -U")
            }
        }
        stage("Build Image") {
            copyJar()
            dir("docker") {
                buildDockerImage(version, env.BRANCH_NAME)
            }
        }
    } catch(error) {
        throw error
    } finally {
        cleanWs()
    }
}