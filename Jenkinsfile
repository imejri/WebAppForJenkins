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
        } // stage
         stage('Print dot net info') {
            steps {
               sh 'dotnet --info'
            } //steps
        } // stage
    } //stagees
} // pipeline
