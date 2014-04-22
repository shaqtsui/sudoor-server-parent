
# Parent Project Profiles:


## Customize Build Process:
### child (active by default in child project)   
* Attach class
* Attach source
* Add failsafe report

### integrationTest
* On pre-integration-test stage perform integrate test. **Note: this must active runtime.appsvr also, since IT rely on server**

### openshift
* Set war output to webapps, so that the war will be deployed by openshift script


## Provide Tool Script:

### runtime.appsvr
* New Appsvr Config

### runtime.appsvr.local
* Local Existing Appsvr Config. **Note: this must active runtime.appsvr also**

### runtime.appsvr.remote
* Remote Existing Appsvr Config. **Note: this must active runtime.appsvr also**

### runtime.appsvr.https
* Config server to listen on https port. **Note: this must active runtime.appsvr also**
* Keys will also generated before server start.

### runtime.appsvr.debug
* Debug Config. **Note: this must active runtime.appsvr also**
