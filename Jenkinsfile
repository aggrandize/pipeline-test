node {
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      checkout scm
      
      // Get the Maven tool.
      env.PATH = "${tool 'M3'}/bin:${env.PATH}"
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "mvn -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/mvn -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Deploy') {
      // Run the maven deploy
      if (isUnix()) {
         sh "mvn wildfly:deploy"
      } else {
         bat(/mvn wildfly:deploy/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}