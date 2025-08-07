pipeline {
    agent { label "jenkins-Agent" }
    environment {
              APP_NAME = "clumsy-pipeline"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                   git branch: 'main', credentialsId: 'GitHub', url: 'https://github.com/corecorie/clumsy-gitops'
               }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   cat deployment.yaml
                   sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "corecorie"
                   git config --global user.email "corecorie0@gmail.com"
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'GitHub', gitToolName: 'Default')]) {
                  sh "git push https://github.com/corecorie/clumsy-gitops main"
                }
            }
        }
      
    }
}
