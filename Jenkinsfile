node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/apotkamp/TDDTrainingApplication.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven339'
//      JAVA_HOME = tool 'JDK8_144'
      env.JAVA_HOME="${tool 'JDK8_144'}"
      env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
   }
   stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "cd TDDTrainingApplicationCC; '${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archive 'target/*.jar'
   }
}
