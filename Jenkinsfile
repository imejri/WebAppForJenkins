pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Upload to Artifactory') {
      //agent {
       // docker {
         // image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
         // reuseNode true
        //}
     // }
      steps {
        sh 'jfrog rt upload --url http://64.225.51.239:8082/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/MyWebApp.war java-web-app/'
      }
    }
  }
}
