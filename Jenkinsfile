node {
  stage('build & deploy') {
    openshiftBuild bldCfg: 'python-flask-alan',
      namespace: 'development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'python-flask-alan',
      namespace: 'development'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('deploy to test') {
    openshiftTag srcStream: 'python-flask-alan',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'testing',
      destStream: 'python-flask-alan',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'python-flask-alan',
      namespace: 'testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('deploy to production') {
    openshiftTag srcStream: 'python-flask-alan',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'production',
      destStream: 'python-flask-alan',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'python-flask-alan',
      namespace: 'production'
  }
}
