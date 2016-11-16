#!groovy
import static org.foo.Utilities.*
node ('worker_node1') {
try {
    stage('Build') {
	  // Run the gradle build
      gbuild this, 'clean build'
   }
   stage ('Test') {
   // execute required unit tests in parallel
   stash name: 'test-sources', includes: 'build.gradle,src/'
   
      parallel (
             node ('master'){
                unstash 'test-sources'
		gbuild this, '-D test.single=TestExample1 test'
             },
             node ('worker_node2'){
  		unstash 'test-sources'
		gbuild this, '-D test.single=TestExample2 test'
             },
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

