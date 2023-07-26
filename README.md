# screenshot
project of screenshot python 

### Fastest way to create server ,by clone existing machine (example  snap-firefox-nl-06.upress.io)
1. create a clone from existing machine in Vsphere

2. log-in to the new machine and change the hostname

3. /root/screenshot/.env change to correct IP

4. restart the service of screenshot 
> systemctl restart sceenshot

5. update the ssh-key in the github repository
> 
6. create ssh-keygen 
example: 
> ssh-keygen -t ed25519 -C  "galina@upress.io"

7. run ssh-agent 
> eval "$(ssh-agent -s)"

8. take the public key , put in inside the GITHUB


### Fresh installation , clone from GitHub

1. python3 installation
> yum install python3

2. install firefox 
> yum install firefox

3. xvfb :
> yum install Xvfb 

4. clone fron github the library
4.1 create ssh-keygen 
example: 
> ssh-keygen -t ed25519 -C  "galina@upress.io"

4.2 run ssh-agent 
> eval "$(ssh-agent -s)"

4.3 take the public key , put in inside the GITHUB 

4.4 clone

> git clone  git@github.com:galina-upress/screenshot.git


5. Activate the VENV
> source /root/screenshot/bin/activate

6. Install prerequired libs in venv
> (screenshot1) [root@galina-work5 screenshot]# pip install selenium xvfbwrapper python-decouple requests Flask

7. download driver for firefox  

https://github.com/mozilla/geckodriver/releases

I used : geckodriver-v0.33.0-linux64.tar.gz

8. edit the  /root/screenshot/.env  to lead to the right path of the driver
```
geckodriver_path = '/root/screenshot/drivers/geckodriver'
```

### Run 
#### Manual run : 
> python3 capture-single.py

#### Run as a service 
1. Edit the file  /lib/systemd/system/screenshot.service

example:
```
#To reload systemd daemon after changes to this file:
#systemctl --system daemon-reload
[Unit]
Description=screenshot driver load and lask app run for listenning
After=network.target

[Service]
Restart=always
Environment=PATH=/usr/bin:/usr/local/bin:/usr/sbin
WorkingDirectory=/root/screenshot
Type=simple
PermissionsStartOnly=true
ExecStart=/root/screenshot/run_screen.sh
RestartSec=5
TimeoutSec=60
PIDFile=/tmp/myFlask.pid
[Install]
WantedBy=multi-user.target
```

2. update the ExecStart=/root/screenshot/run_screen.sh  to correct run script path , and  WorkingDirectory=/root/screenshot  to correct path
   
3. start the sreenshot and enavle it
> systemctl start screenshot

> systemctl enable screenshot
