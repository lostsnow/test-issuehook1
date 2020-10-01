pipeline {
  agent any
  stages {
    stage('start') {
      steps {
        echo 'start'
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
      steps {
        mattermostSend 'sucess'
      }
    }

  }
}