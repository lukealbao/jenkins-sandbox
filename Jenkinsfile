// STATUS
//
// OK! Correct syntax is <VAR>=sh(returnStdout: true, script: '<command>').trim()

pipeline {
  agent any
    // DBNAME=sh 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"'
  environment {
    PGDATABASE=sh(returnStdout: true, script: 'echo "git_$(echo $GIT_COMMIT | head -c7)_build_$BUILD_NUMBER"').trim()
  }
  stages {
    stage('Setup Environment') {
      steps{
        script {
          // env.PGDATABASE=sh(returnStdout: true, script: 'echo "$(echo $GIT_COMMIT | head -c7)_db_$BUILD_NUMBER"').trim()
          PGHOST='localhost'
        }
        nodejs(nodeJSInstallationName: 'node') {
          sh 'npm config ls'
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
          echo "using db ${env.PGDATABASE}"
          // sh "createdb ${env.PGDATABASE}"          
        }
      }
    }

    stage('Run Tests') {
      steps {
        timeout(10) {
          sh 'npm test'
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
  post {
    always {
      junit 'xunit.xml'
    }
  }
}
