#!groovy
import static org.conf.Utilities.*
node ('worker_node1') {
try {
      stage('Source') {
         // always run with a new workspace
         step([$class: 'WsCleanup'])
	 checkout scm
      }
      stage('Build') {
         // Run the gradle build
         gbuild this, 'clean build -x test'
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

