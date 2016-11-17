#!groovy
import static org.foo.Utilities.*
node ('worker_node1') {
   // always run with a new workspace
   step([$class: 'WsCleanup'])
   try {
      stage('Build') {
         // Run the gradle build
         gbuild this, 'clean build -x test'
      }
      stage ('Test') {
      // execute required unit tests in parallel
      
         parallel (
            master: { node ('master'){
               // always run with a new workspace
               step([$class: 'WsCleanup'])
	       gbuild this, '-D test.single=TestExample1 test'
            }},
            worker2: { node ('worker_node2'){
               // always run with a new workspace
               step([$class: 'WsCleanup'])
  	       gbuild this, '-D test.single=TestExample2 test'
            }},
         ) 
      } 
   } 
   catch (err) {
      echo "Caught: ${err}"
   }
   stage ('Notify') {
     // mailUser('<your email address>', "Finished")
   }
}

