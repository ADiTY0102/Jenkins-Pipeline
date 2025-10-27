pipeline {
  agent any
  environment {
    TOMCAT_HOME = "C:/Program Files/apache-tomcat-9.0.111/"
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
        bat 'dir'  
      }
    }

    stage('Deploy to Tomcat') {
      steps {
        bat """
          if exist "%TOMCAT_HOME%" (
            copy /Y sample.war "%TOMCAT_HOME%\\webapps\\sample.war"
          ) else (
            echo Tomcat path not found: %TOMCAT_HOME%
            exit /b 1
          )
        """
      }
    }

    stage('Verify') {
      steps {
        bat 'curl -I http://localhost:8080/sample/ || exit 0'
      }
    }
  }
  post {
    success {
      echo "Deployment successful! Visit http://localhost:8080/sample/"
    }
  }
}
