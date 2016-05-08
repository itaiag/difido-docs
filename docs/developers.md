# Developers

## Building the server from sources

### Prerequisite
* Access to the Difido source repository.
* Java JDK installed and the appropriate environment variables configured.
* Maven 3 exists and the appropriate environment variables configured.
* For direct access to the source repository, a Git client is also required.

### Building

* Download or clone the [Difido repository](https://github.com/itaiag/difido-reports/tree/master/difido-server) 
* Open your operating system console, change folder to the _difido-reports-common_ and run
````
> mvn clean install
````
* Change folder to _difido-server/difido-report-server_ and run again

~~~~
> mvn clean install
~~~~

* If the build went successfully, the server will be in the target folder of the _difido-report-server_ folder. 
