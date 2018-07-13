pipeline {
 agent any

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
        PGDATABASE="${GIT_COMMIT}".take(7) + "_build_${BUILD_NUMBER}"
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
