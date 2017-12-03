pipeline {
  agent {
    label 'master'
  }

  stages {
    stage('Unit Tests') {
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
    }
    stage('Build') {
      steps {
        echo 'Building...'
        sh 'ant -f build.xml -v'
      }
    }
    stage('Deploy') {
      steps {
        sh 'cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangle/all/'
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
    }
  }
}
