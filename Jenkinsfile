#!/usr/bin/env groovy

def gv

pipeline {
    agent any
    stages {
        stage("build image") {
            steps {
                script {
                    echo "building the docker image..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo1', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'docker build -t rishabh9593776/dockerflask-1.0 .'
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh 'docker push rishabh9593776/dockerflask-1.0'
                    }
                }
            }
        
        }

        stage("k8") {
            steps {
                sshagent(['k8']) {
                    sh "scp -o StrictHostKeyChecking=no dockerflask.yaml ubuntu@34.228.8.170:/home/ubuntu"
                script {
                    sh "ssh ubuntu@34.228.8.170 kubectl apply -f dockerflask.yaml"
                    }
                }
            }
        
        }
    }
}
