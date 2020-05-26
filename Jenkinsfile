
node {
   def mvnHome
  stage('Preparation') { 
     git branch: '${BRANCH_NAME}', url: 'https://github.com/Devops-venu/lint-app1.git'
      
      mvnHome = tool 'maven-3.3.9'
   }
   stage('Build') {
      // Run the maven build
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean install sonar:sonar'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
