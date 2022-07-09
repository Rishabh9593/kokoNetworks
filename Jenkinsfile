#!/usr/bin/env groovy

def gv

pipeline {
    agent any
    stages {

        stage("build image") {
            steps {
                script {
                    gv.buildImage()
                }
            }
        }
        
    }
}
