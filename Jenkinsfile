pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('AKIARGWR6CGSTJVCA2QY')
        AWS_SECRET_ACCESS_KEY = credentials('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')
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    def gitUrl = 'https://git-codecommit.ap-south-1.amazonaws.com/v1/repos/Snapcoins'
                    def credentialsId = 'AWS'

                    checkout([$class: 'GitSCM', 
                              branches: [[name: 'main']], 
                              doGenerateSubmoduleConfigurations: false, 
                              extensions: [[$class: 'GitSCMExtension', userRemoteConfigs: [[url: gitUrl]]]], 
                              userRemoteConfigs: [[url: gitUrl, credentialsId: e5354950-0743-49e3-9873-0495dc7066dc]]])
                }
            }
        }

        stage('Build and Test') {
            steps {
                dir('client') {
                    sh 'npm install'
                    // sh 'npm test'
                }

                dir('servers/gamer-module') {
                    sh 'npm install'
                    // sh 'npm test'
                }

                dir('servers/merchant-module') {
                    sh 'npm install'
                    // sh 'npm test'
                }

                dir('servers/gaming-vendor-module') {
                    sh 'npm install'
                    // sh 'npm test'
                }

                dir('servers/general-module') {
                    sh 'npm install'
                    // sh 'npm test'
                }
            }
        }

        stage('Create Docker Images') {
            steps {
                dir('client') {
                    sh 'docker build -t client-image .'
                }

                dir('servers/gamer-module') {
                    sh 'docker build -t gamer-module .'
                }

                dir('servers/merchant-module') {
                    sh 'docker build -t merchant-module .'
                }

                dir('servers/gaming-vendor-module') {
                    sh 'docker build -t gaming-vendor-module .'
                }

                dir('servers/general-module') {
                    sh 'docker build -t general-module .'
                }
            }
        }
    }
}
