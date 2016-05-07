# Running the Difido server with init.d script

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

