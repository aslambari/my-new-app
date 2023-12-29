pipeline {
  agent any
  environment {
	  //adding a comment for the commit test
	  DEPLOY_CREDS = credentials('deploy-anypoint-user')
	  MULE_VERSION = '4.4.0'
	  BG = "Vanshiv"
	  WORKER = "Micro"
	  M2SETTINGS = "C:\\Windows\\system32\\config\\systemprofile\\.m2\\settings.xml"
  }
  
  stages {
	  stage('Build') {
		  steps {
		  	bat 'mvn -B -U -e -V clean -gs %M2SETTINGS% -DskipTests package'
		  }
	  }
	  
	  stage('Test') {
		  steps {
		  	bat "mvn test"
		  }
	  }
	  
	  stage('Deploy Sandbox') {
		  environment {
			  ENVIRONMENT = 'Sandbox'
			  APP_NAME = 'my-new-app'
	  	  }
		  steps {
			  bat 'mvn -U -V -e -B -X -gs %M2SETTINGS% -DskipTests deploy -DmuleDeploy -Dmule.version="%MULE_VERSION%" -Danypoint.username="%DEPLOY_CREDS_USR%" -Danypoint.password="%DEPLOY_CREDS_PSW%" -Dcloudhub.app="%APP_NAME%" -Dcloudhub.environment="%ENVIRONMENT%" -Dcloudhub.bg="%BG%" -Dcloudhub.worker="%WORKER%"'
		 }
	  }
  
  }
  
  
  }
