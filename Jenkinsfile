pipeline {

      agent any
      stages {
            stage('Lint HTML') {
               steps {
                   sh 'tidy -q -e *.html'
               }
          }
	      stage('Build image') {
            steps {
                script {
			sh '''
			docker build --tag ahamed1122/udacity:capstonedocker .
			docker login -u ahamed1122 -p 123456789udacity
			docker push ahamed1122/udacity:capstonedocker
			'''
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
