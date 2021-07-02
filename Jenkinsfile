pipeline {
  environment {
    registry = "Misbah-J/emoji-search"
    registryCredential = 'dockerhub'
    KUBECONFIG="$JENKINS_HOME/.kube/config1"
  }
  agent any
  stages {
    stage('Building image') {
      steps{
        sh "printenv"
        sh "docker build -t misbah012/emoji-search:$BUILD_ID-$BRANCH_NAME ."
       // sh "docker run -dp 80:80 riteshk03/emoji-search:$BUILD_ID-BRANCH_NAME"
        sh "docker push misbah012/emoji-search:$BUILD_ID-$BRANCH_NAME"
      }
    }
   

  stage('Creating Deployment') {
      steps {
    
        sh  '''#!/bin/bash
                
                if [[ $GIT_BRANCH == "misbah-dev" ]]
                then
                    kubectl set image deployment/misbah-new-dep nginx=misbah012/emoji-search:$BUILD_ID-$BRANCH_NAME -n $BRANCH_NAME
                elif [[ $GIT_BRANCH == "misbah-testing" ]]
                then
                    kubectl set image deployment/misbah-new-dep nginx=misbah012/emoji-search:$BUILD_ID-$BRANCH_NAME -n $BRANCH_NAME
                elif [[ $GIT_BRANCH == "misbah-prod" ]]
                then
                    kubectl set image deployment/misbah-new-dep nginx=misbah012/emoji-search:$BUILD_ID-$BRANCH_NAME -n misbah-prod
                   
                fi         
            '''
      }
    }

    stage('') {
      steps{
        sh '''
            kubectl get deployments -n $BRANCH_NAME
            kubectl get svc -n $BRANCH_NAME
            '''
      }
    }
    
    }
}
