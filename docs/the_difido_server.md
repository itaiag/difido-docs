# The Difido Server

## Installation Prerequisite

* Java 8

## Running the Server
[[Download | https://github.com/Top-Q/difido-reports/releases]] and extract the server to your machine 

Start the server by running the script file from the bin folder

~~~
> bin/start.sh
~~~

### Running as Linux service
You may want to run the Difido server immediately after system boot. If this is the case, and you are using some flavor of Linux as the machine OS, adding a startup script to the init.d folder can be a good way to accomplish just that. 

First, you will need a script that can start, stop and restart the server. You can copy the _difido_ script that is located in the bin folder in the _Difido server_ assembly. The script should look something like that:

~~~~sh
#!/bin/bash
# Difido server
#
# description: Script that can be added to the /etc/init.d and will cause the server to run at the init stage. In additions, allows to use the start, stop and restart services. 
# 

readonly DIFIDO_PATH=/usr/local/bin/difido-server

function start {
    cd $DIFIDO_PATH
        /bin/bash bin/start.sh
}

function stop {
    cd $DIFIDO_PATH
        /bin/bash bin/stop.sh

}

case $1 in
    start)
        start
    ;;
    stop)
        stop
    ;;
    restart)
        stop
        start 
    ;;
esac
exit 0

~~~~

In the script, edit the line with the _DIFIDO_PATH_ variable with the location of the server. Save the script and copy it as superuser to the _/etc/init.d_ folder.
Change folder to the /etc/init.d and register your script using the following command

`````
sudo update-rc.d difido defaults
`````

This is it. now the server will be launched automatically after boot and will be closed when the machine is about to shutdown.
In addition, you can start, stop and restart the server using the following commands

``````
/etc/init.d/difido start
``````
``````
/etc/init.d/difido stop
``````
``````
/etc/init.d/difido restart
``````

## Basic Server Configuration

* The server configuration files exist the _config_ folder. Open for edit the _difido_config.properties_ file.

~~~~~
max.execution.idle.time.in.seconds=60  -   The maximum period of time in seconds in which the server is allowed to be idle before closing the current execution.
doc.root.folder=docRoot                -    Location of the static HTML files 
path.data=data/index                   -  Location of the Elasticsearch data
~~~~~

To configure the port and host of the server

### Windows
Open for edit the **bin/start.bat** file and set the values of the **-Dserver.address** and the **-Dserver.port** properties

### Linux
Open for edit the **bin/start.sh* file, search for PORT and HOST variables and set it with your server details.

~~~~~
readonly PORT=8080

readonly HOST=0.0.0.0
~~~~~  


## Basic Client Configuration