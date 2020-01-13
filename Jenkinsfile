node {
  stage('build & deploy') {
    openshiftBuild bldCfg: 'python-flask',
      namespace: 'development',
      showBuildLogs: 'true'
    openshiftVerifyDeployment depCfg: 'python-flask',
      namespace: 'development'
  }
  stage('approval (test)') {
    input message: 'Approve for testing?',
      id: 'approval'
  }
  stage('deploy to test') {
    openshiftTag srcStream: 'python-flask',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'testing',
      destStream: 'python-flask',
      destTag: 'test'
    openshiftVerifyDeployment depCfg: 'python-flask',
      namespace: 'testing'
  }
  stage('approval (production)') {
    input message: 'Approve for production?',
      id: 'approval'
  }
  stage('deploy to production') {
    openshiftTag srcStream: 'python-flask',
      namespace: 'development',
      srcTag: 'latest',
      destinationNamespace: 'production',
      destStream: 'python-flask',
      destTag: 'prod'
    openshiftVerifyDeployment depCfg: 'python-flask',
      namespace: 'production'
  }
}
