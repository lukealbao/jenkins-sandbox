pipeline {
  agent any
  // DBNAME=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
  def DBNAME='hello'
  stages {
        
    stage('Checkout Code') {
      steps {
        timeout(10) {
          deleteDir()
          checkout scm
        }
      }
    }

    stage('Environment Testing') {
      environment {
        PGDATABASE=DBNAME
      }

      steps {
        timeout(10) {
          sh 'echo "PGDATABASE is ${PGDATABASE}"'
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
