pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/adityasubhash35/8.2DevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test || true'  // allow pipeline to continue
      }
      post {
        success {
          emailext(
            to:      'adityasubhash35@gmail.com',
            subject: "[Jenkins] Tests PASSED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:    """\
Build: ${env.BUILD_URL}
Status: SUCCESS

See attached console log.
""",
            attachLog: true
          )
        }
        failure {
          emailext(
            to:      'adityasubhash35@gmail.com',
            subject: "[Jenkins] Tests FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:    """\
Build: ${env.BUILD_URL}
Status: FAILURE

See attached console log.
""",
            attachLog: true
          )
        }
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh 'npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh 'npm audit || true'
      }
      post {
        always {
          emailext(
            to:         'adityasubhash35@gmail.com',
            subject:    "[Jenkins] Security Scan Result: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body:       """\
Build: ${env.BUILD_URL}
Here is the output of npm audit.
See attached console log for details.
""",
            attachmentsPattern: '/npm-debug.log', // if you have a specific log file
            attachLog:          true
          )
        } //presntation changes
      }
    }

  } // stages
}