pipeline {
    agent { label "openshift-common" }
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
                  //node('golang') {
                      withEnv(["PATH+OC=${tool 'oc'}"]) {
                            openshift.withCluster("https://192.168.42.104:8443") {
                             openshift.withProject("cicd") {   
                                 openshift.withCredentials('jenkins-integration') {
                              echo "Hello from project ${openshift.project()} in cluster ${openshift.cluster()}"
                              
                              def dc = openshift.selector('dc', "gitea")
                                dc.rollout().status()
                             }}
                            }
                        }
                      
                  //}
              }
            }
        }
        
    }
}

