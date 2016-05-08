# Running Locally with JSystem

While Difido is intended to use with various testing framework, it has a strong integration with the [JSystem](https://github.com/Top-Q/jsystem) framework.

**Notice:** The remote difido reporter exists only in JSystem version 6.1.01 and up.


## JSystem Side
* Open JSystem
* Open _Tools>JSystem Properties_
* In the _JSystem Properties_ dialog, click on the _Reporter_ tab and open the _reporter.classes_ property
* While keeping the ctrl button clicked, Select the jsystem.extenstions.report.difido.HtmlReporter
* Select the jsystem.extenstions.report.difido.RemoterHtmlReporter
* Unselect the LevelHtmlTestReporter
* Restart the runner

## Configuring the client side
* After restart a new configuration file will be created in the root folder of JSystem with name **remoteDifido.properties**. Open the file and configure the *host* and *port* of the Difido server.


## Usage
* To launch the server click on the *run.bat* file that is located in the *bin* folder
* Open the runner and launch your scenario. If the runner is already running, make sure to init the reports.
* Open your browser and navigate to: \<server host\>:\<server port\>
* Click on the execution and browse the reports
