pipeline {
  agent any
  stages {
    stage('checkout code') {
      steps {
        git(url: 'https://github.com/corecorie/curriculum-app', branch: 'dev')
      }
    }

    stage('fff') {
      steps {
        sh 'ls -la'
      }
    }

  }
}