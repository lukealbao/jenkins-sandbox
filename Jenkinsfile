// STATUS
// seems to be the one that works: stages > X > steps > script > <work>

pipeline {
  agent any
  // DBNAME=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
  stages {
    stage('Setup Environment') {
      steps{
        script {
          PGDATABASE=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
          PGHOST='localhost'
        }
      }
    }  
        
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
          sh "echo using db ${PGDATABASE}"
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
