import java.text.SimpleDateFormat

currentBuild.displayName = new SimpleDateFormat("yy.MM.dd").format(new Date()) + "-" + env.BUILD_NUMBER

env.REPO = "https://github.com/e-lie/tp_fil_rouge_devops_application.git"
// env.IMAGE = "vfarcic/go-demo-3"
// env.ADDRESS = "go-demo-3-${env.BUILD_NUMBER}-${env.BRANCH_NAME}.acme.com"
// env.PROD_ADDRESS = "go-demo-3.acme.com"
// env.TAG = "${currentBuild.displayName}"
// env.TAG_BETA = "${env.TAG}-${env.BRANCH_NAME}"

def nodelabel = "jenkins-slave-${UUID.randomUUID().toString()}"

podTemplate(
  label: nodelabel,
  namespace: "jenkins",
  serviceAccount: "jenkins",
  yaml: """
apiVersion: v1
kind: Pod
metadata:
  labels:
    component: ci
spec:
  containers:
    - name: python
      image: python:3.7
      command:
        - cat
      tty: true
"""
) {
  node(nodelabel) {
    stage("python-test") {
        container('python') {
          git "${env.REPO}"
          sh "pip install -r requirements.txt"
          sh "python tests.py"
        }
    }
  }
}