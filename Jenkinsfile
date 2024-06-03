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
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }
  }
}
