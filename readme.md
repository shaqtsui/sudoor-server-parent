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
	
	on post-integrate-test stage - stop 

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

# Tool Scripts:
*maven-release-plugin
