#  Using Upstart to maintain a long running python process

I recently built a chatbot for slack and wanted to make sure that it kept running on my remote vm.

Luckily you can use upstart to ensure nothing goes awry and even to respawn the process if for some reason it breaks

## Write a config file and store it in /etc/init

```
# chatbot.conf

description "slack service"

start on runlevel [2345]
stop on runlevel [!2345]

# script process w/ logging
exec /home/gregce/anaconda2/bin/python /home/gregce/cxchatbot/cxchatbot.py >> /var/log/chatbot.log 2>&1 

respawn
```

## Do stuff with the new the service 

```
sudo service chatbot start

sudo service chatbot status

sudo service chatbot stop

# cat the logs
cat /var/log/chatbot.log
```
