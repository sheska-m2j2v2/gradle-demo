#!groovy
// @Library('Utilities') import static org.foo.Utilities.*
import static org.foo.Utilities.*

currentBuild.result='SUCCESS'
node ('worker_node1') {
 try {
     stage('Source') { // for display purposes
      // Get some code from our Git repository
      git 'git@diyvb:repos/gradle-greetings.git'
      
   }
  stage ('Build') {
  build this, 'clean build'
  }
  stage ('Verify') {
         // Now load 'verify.groovy'.
    def verifyCall = load("/home/diyuser/shared_libraries/src/verify.groovy")
    timeout(time: 5, unit: 'SECONDS') {
    verifyCall("Please Verify the build")
    }
  }
  stage ('Test') {
  // execute required unit tests in parallel
        parallel (
             node ('master'){
                build this, '-D test.single=TestExample1 test'
             },
             node ('worker_node2'){
                build this, '-D test.single=TestExample2 test'
             },
)

  }

} catch (err) {
        echo "Caught: ${err}"
       
    }

  stage ('mail') {
      mailUser('Brent.Laster@sas.com', currentBuild.result)
      //  mail bcc: '', body: 'The current build\'s result is ${currentBuild.result}', cc: '', from: '', replyTo: '', subject: 'Build Status', to: 'Brent.Laster@sas.com'

      //  mailUser("Brent.Laster@sas.com")
    }
}
