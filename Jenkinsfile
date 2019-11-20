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
                sh 'echo 123'
            }
        }
        stage('Test') {
             steps {
                sh 'echo 456'
            }
        }
        stage('Deploy') {
            steps {
                openshift.withCluster() {
                    sh 'echo "Inside cluster"'
                }
            }
        }
    }
}
