pipeline {
   agent any

   environment {
     //  You must set the following environment variables
     // ORGANIZATION_NAME
     // YOUR_DOCKERHUB_USERNAME (it doesn't matter if you don't have one)

     SERVICE_NAME = "scripts-queue"     
     REPOSITORY_TAG="${YOUR_DOCKERHUB_USERNAME}/${ORGANIZATION_NAME}-${SERVICE_NAME}:${BUILD_ID}"
   }

   stages {
      stage('Preparation') {
         steps {
            cleanWs()
            git credentialsId: 'GitHub', url: "https://github.com/${ORGANIZATION_NAME}/${SERVICE_NAME}"
         }
      }
      stage('Build') {
         steps {
            sh '''echo No build required...queue'''
         }
      }

      stage('Build and Push Image') {
         steps {
           sh 'echo No docker image for...queue'
         }
      }

      stage('Deploy to Cluster') {
          steps {
                // withKubeConfig(contextName: 'default', credentialsId: '9a91910b-c106-47bc-bc12-757dfd2ad6a2', namespace: 'default', serverUrl: '${KUBERNETES_API_SERVER}') {
                    sh 'envsubst < ${WORKSPACE}/rabbit-rbac.yaml | kubectl apply -f -'
                    sh 'envsubst < ${WORKSPACE}/rabbit-secret.yaml | kubectl apply -f -'
                    sh 'envsubst < ${WORKSPACE}/rabbit-configmap.yaml | kubectl apply -f -'
                    sh 'envsubst < ${WORKSPACE}/rabbit-statefulset.yaml | kubectl apply -f -'
                   
                // }
          }
      }
   }
}
