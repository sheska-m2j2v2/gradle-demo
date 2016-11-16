#!groovy
import static org.foo.Utilities.*
node ('worker_node1') {
try {
   def gradleHome
   stage('Source') { // for display purposes
      // Get some code from our Git repository
      git 'git@diyvb:repos/gradle-greetings.git'
   }
   stage('Build') {
	  // Run the gradle build
      gbuild this, 'clean build'
   }
   stage ('Test') {
   // execute required unit tests in parallel
   
      parallel (
             node ('master'){
		gbuild this, '-D test.single=TestExample1 test'
             },
             node ('worker_node2'){
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

