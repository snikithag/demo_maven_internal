pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Setup') {
      steps {
        script {
          if (isUnix()) {
            sh 'mkdir -p target test-results'
            sh 'python3 -m pip install --upgrade pip'
            sh 'python3 -m pip install -r requirements.txt'
          } else {
            bat 'if not exist target mkdir target'
            bat 'if not exist test-results mkdir test-results'
            bat 'python -m pip install --upgrade pip'
            bat 'python -m pip install -r requirements.txt'
          }
        }
      }
    }
    stage('Build and Test') {
      steps {
        script {
          if (isUnix()) {
            sh 'python3 hello.py > target/output.txt'
            sh 'pytest --junitxml=test-results/results.xml'
          } else {
            bat 'python hello.py > target\\output.txt'
            bat 'pytest --junitxml=test-results\\results.xml'
          }
        }
      }
    }
    stage('Artifact') {
      steps {
        junit 'test-results/**/*.xml'
        archiveArtifacts artifacts: 'target/**', fingerprint: true
      }
    }
  }
}
