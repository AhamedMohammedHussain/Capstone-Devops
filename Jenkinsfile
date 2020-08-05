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
                  sh'''docker build --tag ahamed1122/udacity .'''
              }
         }
      }
}
