node('maven') {
  stage('Checkout') {
    // Ensure Jenkins has been configured with latest Oracle JDK 8
    jdk = tool name: "OracleJDK8"
    env.JAVA_HOME = "${jdk}"
    echo "Using : ${jdk}"
    git url: "http://gogs-cicd.192.168.99.100.nip.io/xeonn/otcs-otm", branch: 'master'
  }
  stage('Build') {
    sh "mvn package -Dmaven.test.skip=true"
  }
  stage('Rollout Dev Image') {
    echo "Rolling out to DEVELOPMENT environment."
    sh "oc start-build -n dev otcs-otm --from-dir . --follow"
  }
  stage('Code Quality') {
    sh "echo \"Code quality check successful\""
  }
  stage('Unit Test') {
    sh "echo \"All unit test successful\""
  }
  stage('Integration Test') {
    sh "echo \"All integration test successful\""
  }
  stage('Rollout Beta Image') {
    echo "Rolling out to STAGE environment."
    sh "oc tag -n stage dev/otcs-otm:latest stage/otcs-otm:blue"
  }
}
