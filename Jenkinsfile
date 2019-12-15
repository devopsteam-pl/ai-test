def worker_label = "worker-${UUID.randomUUID().toString()}"
//def ver = sh 'echo 1 | base64'
podTemplate(
    label: worker_label,
    cloud: "openshift",
    inheritFrom: "maven", 
    containers: [
        containerTemplate(
            name: 'jnlp', 
            image: 'openshift/jenkins-slave-base-centos7', 
            command: '',
            workingDir: '/tmp',
            ttyEnabled: false),
    ],
    volumes: [
        //hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
    ]
) {
    node(worker_label) {
        // def myRepo = checkout scm
        // def gitCommit = myRepo.GIT_COMMIT
        // def gitBranch = myRepo.GIT_BRANCH
        // def shortGitCommit = "${gitCommit[0..10]}"
        // def previousGitCommit = sh(script: "git rev-parse ${gitCommit}~", returnStdout: true)
        //sh 'oc get pods'
        def template = """
apiVersion: v1
kind: List
items:
  - apiVersion: v1
    kind: DeploymentConfig
    metadata:
      name: myapp
    spec:
      replicas: 1
      template:
        metadata:
          labels:
            app: myapp
        spec:
          containers:
            - name: basic
              image: busybox:latest
              imagePullPolicy: Always
              command: ['sh', '-c', 'echo The app is running! && sleep 3600']
"""

    stage('Deploy') {
        println tag
    try {
        openshift.withCluster() {
          openshift.withProject() {
               //println "TEMPLATE:" + template.items[]
               echo "Using project: ${openshift.project()}"
               //def template = openshift.process(template_in)
               //openshift.apply(template)
               def dc = openshift.apply(template).narrow("dc")
               //println openshift.get('items')
               //def dc = openshift.selector("dc", 'myapp').narrow("dc")
            
                
            
            def rm = dc.rollout()
		    rm.latest()
			echo 'Getting Status'
		    // Wait and print status
			println "STATUS: " + rm.status().status
			println "STATUS: " + dc.object().status
          }
        }
    }
    catch (Exception e) {
	        echo 'Rollout failed.'
	        error e.getMessage()
        }
    }}
}

println currentBuild.currentResult
