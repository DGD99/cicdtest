pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/mid7098/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t mid7098/testweb:newnewmain .
        sudo docker push mid7098/testweb:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
	sudo kubectl set image deployment deploy-main ctn-main=mid7098/testweb:newnewmain
        '''
      }
    }
  }
}
