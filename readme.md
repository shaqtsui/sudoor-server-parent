# Parent Project Profiles

## Customize Build Process
### child (active by default in child project)   
* Attach class
* Attach source
* Add failsafe report

### integrationTest
* On pre-integration-test stage perform integrate test. **Note: this must active runtime.appsvr also, since IT rely on server**

### openshift
* Set war output to webapps, so that the war will be deployed by openshift script

### runtime.appsvr
* Customize build:

	on pre-integrate-test stage - start/run server

* Appsvr Config, also can directly used as tool script

### runtime.appsvr.local
* Local Existing Appsvr Config. **Note: this must active runtime.appsvr also**

### runtime.appsvr.remote
* Remote Existing Appsvr Config. **Note: this must active runtime.appsvr also**

### runtime.appsvr.https
* Config server to listen on https port. **Note: this must active runtime.appsvr also**
* Keys will also generated before server start.

### runtime.appsvr.debug
* Debug Config. **Note: this must active runtime.appsvr also**

### runtime.appsvr.nostop
* Start Server & don't stop it. **Note: this must active runtime.appsvr also**

# Tool Scripts:
*maven-release-plugin


# Usage Example
	
Run Server & Deploy:
	mvn install -P runtime.appsvr,deploy.app,runtime.appsvr.nostop
	
Run Server in Debug & Deploy:
	mvn install -P runtime.appsvr,deploy.app,runtime.appsvr.nostop,runtime.appsvr.debug
	
Start Server & Integration Test:
	mvn install -P runtime.appsvr,deploy.app,test.integration

Start Server & Performance Test:	
	mvn install -P runtime.appsvr,deploy.app,test.performance
	
	