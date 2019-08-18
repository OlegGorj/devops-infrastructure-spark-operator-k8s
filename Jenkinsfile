pipeline {
  agent {
    kubernetes {
      label 'jenkins-worker'
      defaultContainer 'jnlp'
      yamlFile 'JenkinsPod.yaml'
    }
  }
  stages {

    /*========================================================================*/
    stage('Deploying') {
      when {
        branch 'master'
      }
      steps {
        container('helm') {
          sh(script: "helm init -c --skip-refresh", label: "Initializing Helm Client")
          sh(script: "helm upgrade --install spark-operator ./charts/spark-operator --values=./charts/spark-operator/config.yaml --atomic --namespace=spark-operator", label: "Atomically Deploying Helm Chart")
        }
      }
    }
    /*========================================================================*/

  }
}
