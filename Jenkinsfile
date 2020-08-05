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
                  docker build --tag ahamed1122/udacity:capstonedocker .
              }
         }
      }
}
