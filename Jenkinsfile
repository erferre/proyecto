pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  stages {
    stage('Build') {
	  agent { label 'Docker Node V2' }
      steps {
        sh 'sudo docker build -t jmferreiradk/kube-test .'
      }
    }
    stage('Push') {
      agent { label 'Docker Node V2' }
      steps {
        sh 'sudo docker push jmferreiradk/kube-test'
      }
    }
  }
  post {
    always {
      agent { label 'Docker Node V2' }
      sh 'sudo docker logout'
    }
  }
}
