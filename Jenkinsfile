// STATUS
//
// OK! Correct syntax is <VAR>=sh(returnStdout: true, script: '<command>').trim()

pipeline {
  agent any

  environment {
    PGDATABASE=sh(
      returnStdout: true,
      script: 'echo "git_$(echo $GIT_COMMIT | head -c7)_build_$BUILD_NUMBER"'
    ).trim()
  }
  
  stages {
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
          sh 'echo "MYUSER:${PGPASSWORD}" > .mypassfile'
          echo "using db ${env.PGDATABASE}"
          echo "direct echo ${PGDATABASE}"
          sh 'echo "shell echo ${PGDATABASE}"'
        }
      }
    }

    stage('Run Tests') {
      steps {
        nodejs(nodeJSInstallationName: 'node') {
          sh 'npm test'
        }
      }
    }
  }
  
  post {
    always {
      junit 'xunit.xml'
      // deleteDir()
    }
  }
}
