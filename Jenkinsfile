pipeline {

      agent any
      stages {
            stage('Lint HTML') {
               steps {
                   sh 'tidy -q -e *.html'
               }
          }
	  stage('Build Docker Image') {
              steps {
                  sh 'docker build --tag ahamed1122/udacity:capstonedocker .'
		      
              }
         }
         stage('Push to Dockerhub') {
              steps {
                  echo 'Pushing Image....'
                  withDockerRegistry([url: "", credentialsId: "dockerhub"]) {
                      sh 'docker push ahamed1122/udacity:capstonedocker'
                  }
              }
         }

          stage('Deploy App') {
            steps {
		    withAWS(credentials: 'aws-static', region: 'us-east-1') {
 			sh '''
			aws eks --region us-east-1 update-kubeconfig --name KubsCluster
			kubectl apply -f ./kubernetes-config.yml
            		kubectl get deployments
			'''
		    }
                 }
            }
      }
}
