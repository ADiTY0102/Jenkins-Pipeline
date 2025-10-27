pipeline {
 agent any
 environment {
 TOMCAT_HOME = "C:\Program Files\apache-tomcat-9.0.111\" // Update as needed
 }
 stages {
 stage('Checkout') {
 steps {
 checkout scm
 echo "Checked out repository"
 }
 }
 stage('Prepare') {
 steps {
 sh 'ls -la'
 }
 }
 stage('Deploy to Tomcat') {
 steps {
 sh '''
 if [ -d "${TOMCAT_HOME}" ]; then
 cp -f sample.war ${TOMCAT_HOME}/webapps/sample.war
 touch ${TOMCAT_HOME}/webapps/sample.war
 else
 echo "Tomcat path not found: ${TOMCAT_HOME}"
 exit 1
 fi
 '''
 }
 }
 stage('Verify') {
 steps {
 sleep 10
 sh 'curl -I --max-time 5 http://localhost:8080/sample/ || true'
 }
 }
 }
 post {
 success {
 echo "Deployment successful! Visit: http://localhost:8080/sample/"
 }
 }
}
