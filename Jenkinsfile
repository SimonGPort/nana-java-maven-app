library identifier: 'jenkins-shared-library@main', retriever: modernSCM(
    [$class:'GitSCMSource',
    remote:'https://github.com/SimonGPort/jenkins-shared-library.git'
    credentialsId:'docker-hub-repo'
    ]
)

def gv

pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
         stage("test") {
            steps {
                script {
                     echo "testing the application..."
                }
            }
        }
        stage("build jar") {
            // when{
            //     expression{
            //     BRANCH_NAME=='main'
            //     }
            // }
            steps {
                script {
                     buildJar()
                }
            }
        }
        stage("build image") {
            // when{
            //     expression{
            //     BRANCH_NAME=='main'
            //     }
            // }
            steps {
                script {
                  buildImage 'simongport/my-repo:jma-3.0'
                  dockerLogin()
                  dockerPush 'simongport/my-repo:jma-3.0'
                    }
                }
            }
        stage("deploy") {
            // when{
            //     expression{
            //     BRANCH_NAME=='main'
            //     }
            // }
            steps {
                script {
                    gv.deployApp()
                    }
                }
            }
        }
    }   
