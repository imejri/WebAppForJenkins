pipeline {
    agent any
    tools {
        maven "localMaven"
    }
    stages {
        stage('Clean and Install') {
            steps {
               sh 'mvn clean install'
            }
        }
        stage('Package') {
            steps {
               sh 'mvn package'
            } //steps
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', fingerprint: true, followSymlinks: false
                }
            }
        } // stage
         stage('Print dot net info') {
            steps {
               sh 'dotnet --info'
            } //steps
        } // stage
    } //stagees
} // pipeline
