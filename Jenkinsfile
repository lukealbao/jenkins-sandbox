// STATUS
// I tried to build with a top-level environment, since that is documented
// in the Jenkins docs (https://jenkins.io/doc/pipeline/tour/environment/),
// but it appers you can't use a shell command to apply it.

pipeline {
  agent any
    script {
        env.PGDATABASE=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
    }
  // DBNAME=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
  stages {
    // stage('Setup Environment') {
    //   steps{
    //     script {
    //       env.PGDATABASE=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
    //       env.PGHOST='localhost'
    //     }
    //   }
    // }  
        
    stage('Checkout Code') {
      steps {
        timeout(10) {
          deleteDir()
          checkout scm
        }
      }
    }

    stage('Create database') {
      steps {
        timeout(10) {
          sh "echo using db ${env.PGDATABASE}"
          // sh "createdb ${env.PGDATABASE}"          
        }
      }
    }

    stage('Cleanup') {
      steps {
        timeout(10) {
          deleteDir()
        }
      }
    }
  }
}
