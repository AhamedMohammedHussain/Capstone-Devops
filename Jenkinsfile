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
			dockerImage = docker.build('krravindra/kubernetes-clusters-demo:lastest')
                    docker.withRegistry('', 'dockerhub') {
                        dockerImage.push()
                    }
		}	
		}
          }


          stage('Deploy App') {
            steps {
 			sh '''
			aws eks --region us-east-1 update-kubeconfig --name KubsCluster
			kubectl apply -f ./kubernetes-config.yml
            		kubectl get deployments
			'''
                 }
            }
      }
}
