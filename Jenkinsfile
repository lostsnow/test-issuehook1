pipeline {
  agent any
  stages {
    stage('start') {
      steps {
        echo 'start'
        git(url: 'https://github.com/lostsnow/test-issuehook1.git', branch: 'master', changelog: true)
      }
    }

    stage('run') {
      steps {
        sh 'echo "run"'
      }
    }

    stage('done') {
      steps {
        archiveArtifacts '**/*'
      }
    }

    stage('notify') {
      environment {
        result = 'success'
      }
      parallel {
        stage('notify') {
          steps {
            mattermostSend 'SUCCESSFUL: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\' (${env.BUILD_URL})'
          }
        }

        stage('notifyFail') {
          steps {
            mattermostSend 'FAILED: Job \'${env.JOB_NAME} [${env.BUILD_NUMBER}]\' (${env.BUILD_URL})'
          }
        }

      }
    }

    stage('clean') {
      steps {
        cleanWs(disableDeferredWipeout: true, deleteDirs: true, cleanupMatrixParent: true, cleanWhenUnstable: true, cleanWhenNotBuilt: true, cleanWhenAborted: true, cleanWhenFailure: true, cleanWhenSuccess: true, notFailBuild: true)
      }
    }

  }
}