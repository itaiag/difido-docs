# Running with JSystem

While Difido is intended to use with various testing framework, it has a strong integration with the [JSystem](https://github.com/Top-Q/jsystem) framework.

**Notice:** The remote difido reporter exists only in JSystem [[version 6.1.03|https://github.com/Top-Q/jsystem/releases]] and up.


## JSystem Side

* Open JSystem
* Open _Tools>JSystem Properties_
* In the _JSystem Properties_ dialog, click on the _Reporter_ tab and open the _reporter.classes_ property
* While keeping the ctrl button clicked, Select the jsystem.extenstions.report.difido.HtmlReporter
* Select the jsystem.extenstions.report.difido.RemoterHtmlReporter
* If selected, unselect the LevelHtmlTestReporter
* Still in the _JSystem Properties_ dialog, click on the _New Features_ tab and open the _add.generic.tabs_ property
* Select the _jsystem.treeui.genericTabs.RemoteDifidoPropertiesTab_ 
* Restart the runner

## Configuring the client side
* After restart a new configuration file will be created in the root folder of JSystem with name **remoteDifido.properties**. You can configure the server details directly by editing the file, or, if you find it more convenient, a new tab is also added to JSystem **Remote Difido Properties**. 
Configure the _host_ and _port_ of the Difido server.


