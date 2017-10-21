 # cf-push

 * This is a Cisco Cloud Center external service example to deploy an Cloud Foundry Application
 * Cloud Foundry is a PaaS system, so what we are doing is front ending the Login and Push
   Process with a Cloud Center button that will ask for all the needed information to deploy
   an application into the Cloud Foundry PaaS platform.  
 
 * This service leverages the default Cloud Foundry CLI commands as well as the default ENV vars that CF uses
   for login, password, Organization, Space, API endpoint.  I have defined them below. 
   
   Lastly this service ONLY pulls from GIT today, that was the easiest way to get it working and
   should be where all code is stored anyhow.  And it FREE

 ### Cloud Foundry env vars to be used or mapped into Cloud Center

	*	$CF_API - API endpoint of cloud foundry instance  
	*	$CF_USER - User name in cloud foundry
	*	$CF_PASS - Password
	*	$CF_ORG - Org
	*	$CF_SPACE - Space
	*	$CF_APP_URL - URL to HTTP location to grab application
	*	$CF_APP_NAME - App name in CF that we are creating 
	*	$APP_DIR - name of the applications directory
	*   $APP_BUILD_TYPE - type of application to compile, mavin, gradle, python, static

### Cloud Foundry Push

	* cf login -a $CF_API -u $CF_USER -p $CF_PASS -o $CF_ORG -s $CF_SPACE > cflogin.log
	* git clone $CF_APP_URL
          - APP_DIR=$(echo $CF_APP_URL | sed 's/.*\///')
          - cd $APP_DIR
          - ./gradlew clean assemble
          - cf push $CF_APP_NAME

