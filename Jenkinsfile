pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build initiated'
      }
    }

    stage('Test Stage') {
      parallel {
        stage('Linux Test') {
          steps {
            echo 'Testing in Linux env'
          }
        }

        stage('Windows Test') {
          steps {
            echo 'Testing in windows env'
          }
        }

      }
    }

    stage('Deploy staging') {
      steps {
        echo 'Deploying to staging env'
        input 'Press OK to deploy to production'
      }
    }

    stage('Deploy Production') {
      steps {
        echo 'Deploy to production'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-vidushi.bansal@knoldus.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}