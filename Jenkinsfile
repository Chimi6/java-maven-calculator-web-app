node {
   
   def mvnHome = tool 'M3'
   
   docker.image('jenkins/jenkins').inside {
      
   stage('Checkout Code') { 
      git 'https://github.com/PranayP86/java-maven-calculator-web-app.git'
   }
   stage('JUnit Test') {
      sh "'${mvnHome}/bin/mvn' clean test"
   }
   stage('Integration Test') {
      sh "'${mvnHome}/bin/mvn' integration-test"
     
   }
 /*
   stage('Performance Test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' cargo:start verify cargo:stop"
      } else {
         bat(/"${mvnHome}\bin\mvn" cargo:start verify cargo:stop/)
      }
   }
  */
  stage('Performance Test') {
      sh "'${mvnHome}/bin/mvn' verify"
   }
   stage('Deploy') {
      timeout(time: 10, unit: 'MINUTES') {
           input message: 'Deploy this web app to production ?'
      }
      echo 'Deploy...'
   }
 }
}
