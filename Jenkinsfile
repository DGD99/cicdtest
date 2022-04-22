pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/DGD99/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
	sudo sed -i 's/MAIN/blog/' index.html
        sudo docker build -t mid7098/testweb:newblog .
        sudo docker push mid7098/testweb:newblog
	sudo sed -i 's/blog/shop/' index.html
        sudo docker build -t mid7098/testweb:newshop .
        sudo docker push mid7098/testweb:newshop
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
        sudo kauth
	sudo kubectl set image deployment deploy-blog ctn-blog=mid7098/testweb:newblog
	sudo kubectl set image deployment deploy-shop ctn-shop=mid7098/testweb:newshop
        '''
      }
    }
  }
}
