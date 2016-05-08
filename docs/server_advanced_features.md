# Server Advanced Features

## Execution Properties

You have the ability to add more information on each execution, like execution description and custom properties. 

The information is then shown in the *Execution List*. The description will be shown instead of the link to the execution HTML reports and the properties will be shown as additional columns in the table. 

If you want to avoid stressing the table and limit the type of properties you can configure the allowed properties in the server configuration file as described later on.

### Adding Properties from the API
In the create new execution api, you can pass *Execution Details* json. In the json you can add *description* field from type string and a list of key value pairs (map), that describes the execution properties. 

More information can be found on the [[API Page|Server-API]].

## Adding properties from JSystem
Difido can work with various frameworks, but a good usage example is the integration with the JSystem framework. 
To configure the execution description and properties from JSystem, simply edit the *remoteDifido.properties* file that is created in the root of the runner.

In the file you can add values to the following fields:

````
execution.description=Deposit Center Tests
execution.properties=user=Itai;env=qa03;version=6.32.0123
````

In the *execution.description* field, you can add the description of the execution and in the *execution.properties* you can add a semicolon separated list of key values. 
Notice that this file is read only when the JSystem is launched, so you will need to restart the runner in order for any changes to take affect.

### Filtering properties
Since every execution property is added as a new column to the execution list table, You may not want to permit every user to add any execution property.

To filter the properties, shutdown the server, open for edit the configuration file (difido_config.properties), and locate the *custom.execution.properties* field.
You can now add the allowed properties as semicolon separated list of values

````
custom.execution.properties=user;env;version
````

After relaunching the server, only properties with the specified keys will be added to the executions. 

**Notice:** if the list is empty or if the field does not exist in the configuration file, all properties will be allowed. 


## Sending mails from the Difido server

The Difido server now supports sending mails at the end of the execution. The mail can contain different attributes of the execution like the overall, failed and warning tests in the execution, the number of machines that were reported to it and a link to the HTML report.


### Configuring SMTP details

To enable it, you will need to enable sending mails and to specify your organization SMTP details in the *difido_config.properties* configuration file

For example:

~~~~
enable.mail=true
mail.ssl=true
mail.to.address=destination@mycompany.com
mail.from.address=source@mycompany.com
mail.smtp.host=smtphost
mail.smtp.port=25
mail.user.name=myusername
mail.password=mysecretpassword
mail.cc.address=otherdestination@mycompany.com
~~~~

If you want to send mail from a Gmail address, you configuration should look something like this:

~~~~
enable.mail=true
mail.ssl=true
mail.to.address=destination@gmail.com
mail.from.address=source@gmail.com
mail.smtp.host=smtp.gmail.com
mail.smtp.port=587
mail.user.name=myusername@gmail.com
mail.password=mysecretpassword
mail.cc.address=otherdestination@gmail.com
~~~~

**IMPORTANT:** You will probably also need to change your Gmail settings and to [allow access for less secure apps](https://www.google.com/settings/security/lesssecureapps).

### Changing the mail body

You can also change the template of the mail body. The template file *mail.vm* is kept in the *configuration* folder.
The server is using [Velocity](https://velocity.apache.org/) as the template language, so you can use all the power of it for creating more interesting messages.
The main object that you can use in your template is called $meta, and it has the following members:

~~~~java

		/**
		 * The id of the execution
		 */
		private int id;

		/**
		 * The name of the folder in the file system that holds the report file.<br>
		 * e.g. execution_2015_04_14__22_15_38_84 <br>
		 */
		private String folderName;

		/**
		 * The uri of the index file of the execution report. <br>
		 * e.g. reports/execution_2015_04_14__22_15_38_84/index.html
		 */
		private String uri;

		/**
		 * The date in which the execution was created in. <br>
		 * e.g. 16/10/2016
		 */
		private String date;

		/**
		 * The time in which the execution was created in. <br>
		 * 12:32:11:23
		 */
		private String time;

		/**
		 * Is the execution is currently active or is it already finished
		 */
		private boolean active;

		/**
		 * The last time in absolute nanoseconds that this execution was
		 * changed. This is used for calculating if the max idle time is over
		 */
		private long lastAccessedTime;

		/**
		 * Overall number of tests in the execution
		 */
		private int numOfTests;

		/**
		 * Number of successful tests in the execution
		 */
		private int numOfSuccessfulTests;

		/**
		 * Number of failed tests in the execution
		 */
		private int numOfFailedTests;

		/**
		 * Number of tests with warnings in the execution
		 */
		private int numOfTestsWithWarnings;

		/**
		 * Number of machines that were reported to this execution
		 */
		private int numOfMachines;

		/**
		 * The date and time in which the execution has started in. e.g.
		 * 2015/05/12 18:17:49
		 */
		private String timestamp;

~~~~

## ElasticSearch and Kibana

* To integrate Kibana, [download](https://www.elastic.co/downloads/kibana) and extract it to your machine
* Launch it by running the *kibana.bat* file that is located in the Kibana bin folder.
* Open your browser and navigate to: \<Kibana host\>:5601
* At the *settings->indices* page, select **report***  as the index name.
* In the *Time-field name*, select the **executionTimestamp** field.

## Shared Executions