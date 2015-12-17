# A simple Upstart script

From the Upstart page http://upstart.ubuntu.com/

> Upstart ... handles starting of tasks and services during boot, stopping them during shutdown and supervising them while the system is running.

For my simple script I want to ensure that my Node.js server is started when the server boots (so it survives restarts). I could also make sure it is shut down gracefully when the server is restarting.

## Stanzas

I found the key to understanding Upstart scripts is to understand that they contain commands called stanzas, these are defined at http://upstart.ubuntu.com/wiki/Stanzas.

## Simple script

The file is named **example-node-server.conf** and placed in /etc/init.

Once in this folder the job will be automatically run by upstart depending on the events you've defined.

You can manually start/stop this job with the start/stop/restart/status commands, for example to stop and start:

`sudo service example-node-server restart`

Here's my script, compare this with the satanza page linked above and it should make sense.

```
description "Upstart Script for my Example Node Server"
#output is logged to: /var/log/upstart/example-node-server.log
#upstart "stanzas" are explained here: http://upstart.ubuntu.com/wiki/Stanzas

start on filesystem or runlevel [2345]
stop on shutdown

env APP_DIR=/home/jonathan/example-node-server

# this specifies what will be run for the job, it contains shell script executed with /bin/sh (with -e so errors will terminate the script at once)
script
        chdir $APP_DIR
        exec bash -c 'source /home/jonathan/example-node-server/.nvm/nvm.sh && nvm install && exec node .'
end script

pre-start script
        echo "[`date`] Example Server Starting"
end script

pre-stop script
        echo "[`date`] Example Server Stopping"
end script
```

### More information
https://www.digitalocean.com/community/tutorials/the-upstart-event-system-what-it-is-and-how-to-use-it

http://upstart.ubuntu.com/

http://upstart.ubuntu.com/wiki/Stanzas
