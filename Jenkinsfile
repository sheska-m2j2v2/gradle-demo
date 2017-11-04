#!groovy
@Library('Utilities@1.5')_
node ('worker_node1') {
try {
      stage('Source') {
         // always run with a new workspace
         cleanWs()
	 checkout scm
      }
      stage('Build') {
         // Run the gradle build
         gbuild2 'clean build -x test'
      }
      stage ('Test') {
         // execute required unit tests in parallel
              
      } 
   } 
   catch (err) {
      echo "Caught: ${err}"
   }
   stage ('Notify') {
      // mailUser('<your email address>', "Finished")
   }
}


