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
  
 

   }

}  // end try
catch (err) {
   echo "Caught: ${err}"
}
   stage ('Notify') {
    // mailUser('<your email address>', "Finished")
   }
}

