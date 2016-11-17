#!groovy
import static org.foo.Utilities.*
node ('worker_node1') {
try {
    stage('Build') {
       // Run the gradle build
      gbuild this, 'clean build -x test'
   }
   stage ('Test') {
   // execute required unit tests in parallel
      
      parallel (
             master: { node ('master'){
              	gbuild this, '-D test.single=TestExample1 test'
             }},
             worker2: { node ('worker_node2'){
  		gbuild this, '-D test.single=TestExample2 test'
             }},
       )

    }

}  // end try
catch (err) {
   echo "Caught: ${err}"
}
   stage ('Notify') {
     // mailUser('<your email address>', "Finished")
   }
}

