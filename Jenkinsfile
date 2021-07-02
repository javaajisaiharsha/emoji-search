pipeline {
  environment {
    registry = "Misbah-J/sample-app"
    registryCredential = 'dockerhub'
    KUBECONFIG="$JENKINS_HOME/.kube/config1"
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        sh "printenv"
        sh "docker build -t misbah012/emoji-search:$BUILD_ID ."
       // sh "docker run -dp 80:80 riteshk03/emoji-search:$BUILD_ID"
        sh "docker push misbah012/emoji-search:$BUILD_ID"
      }
    }
   

    stage('Creating Deployment') {
      steps {
        sh  '''
            kubectl set image deployment/misbah-new-dep nginx=misbah012/emoji-search:$BUILD_ID
            '''
      }
    }

    stage('') {
      steps{
        sh '''
            kubectl get deployments
            kubectl get svc
            '''
      }
    }
    }
}
