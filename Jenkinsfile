pipeline {
   agent any

  environment {
    JAVA_HOME = '/usr/local/Cellar/openjdk@11/11.0.5+10/libexec/openjdk.jdk/Contents/Home'

  }
   tools {
      // Install the Maven version configured as "M3" and add it to the path.
      gradle "gradle"

   }

   stages {
      stage('checkout') {
          steps {
           // Get some code from a GitHub repository
            git 'https://github.com/mstittle/cidemo.git'
          }
      }
      stage('Build') {
         steps {
       
            // Run Maven on a Unix agent.
            sh "gradle build"

            // To run Maven on a Windows agent, use
            // bat "mvn -Dmaven.test.failure.ignore=true clean package"
         }

         post {
            // If Maven was able to run the tests, even if some of the test
            // failed, record the test results and archive the jar file.
            success {
               archiveArtifacts 'build/libs/*.jar'
            }
         }
      }
   }
}
