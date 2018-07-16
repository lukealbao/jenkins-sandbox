// STATUS
// <VAR> = sh '<command>' syntax leaves <VAR> null. Let's try piping it.

pipeline {
  agent any
  // DBNAME=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
  stages {
    stage('Setup Environment') {
      steps{
        script {
          PGDATABASE=sh(returnStdout: true, script: 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"').trim()
          PGHOST='localhost'
        }
        echo "after assigning value is ${PGDATABASE}"
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
          echo "using db ${PGDATABASE}"
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
