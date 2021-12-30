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
    stage ('config SSH') {
      steps {
        echo "config application"
        script {
          def remote = [:]
remote.name = "artifactory-server"
remote.host = "64.225.51.239"
remote.allowAnyHosts = true

node {
    withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
        remote.user = root
        remote.identityFile = identity
        stage("SSH Steps Rocks!") {
            writeFile file: 'abc.sh', text: 'ls'
            sshCommand remote: remote, command: 'touch /root/issam.txt'
        } // stage
    } // withcredentials
} // node
        } // script
      } // steps
    } // stage
    
    stage('Upload to Artifactory') {
      //agent {
       // docker {
         // image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
         // reuseNode true
        //}
     // }
      steps {
        sh 'jfrog rt upload --url http://64.225.51.239:8082/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/MyWebApp.war java-web-app-libs-release-local/'
      }
    }
  }
}
