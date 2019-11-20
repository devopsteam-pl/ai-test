pipeline {
    agent { label "golang" }
    options { skipDefaultCheckout() }
    stages {
        stage('CleanWorkspace') {
            steps {
                deleteDir()
            }
        }
        stage('Build') {
            steps {
              script {
                            openshift.withCluster() {
                              sh 'echo 123'
                            }
                        }
            }
        }
    }
}
