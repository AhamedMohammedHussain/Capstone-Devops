pipeline {
	environment {
    registry = "ahamed1122/udacity:capstonedocker"
    registryCredential = 'dockerhub' 
  }
      agent any
      stages {
            stage('Lint HTML') {
               steps {
                   sh 'tidy -q -e *.html'
               }
          }
	 
	    stage('Deploy Image') {
	      steps{
		script {
		dockerImage="ahamed1122/udacity:capstonedocker"
		  docker.withRegistry( '', "dockerhub") {
		    dockerImage.push()
		  }
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
