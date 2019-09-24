# pibeat Setup Guide

At the time of creating this script, Elastic has not released an ARM version of Filebeat, so it is necessary to build a 
working version of Filebeat.  Testing was performed on Raspberry Pi 3.+ and Raspberry Pi 4.  

System information for both is listed below with the commands to lookup the info on your system. If your system does not match
the following information, you may need to make some modifications.

**Operating System**

```cat /etc/issue```
OS - Raspbian GNU/Linux 10
OS = Raspbian GNU/Linux 10 \n 1

```cat /etc/debian_version```
10.0
10.1

```python -V ```
Python 2.7.16

```python3 -V ```
Python 3.7.3

```git --version ```
git version 2.20.1

# TODO: This is still a work in progress.

- Still have edits to script to ouput to log
- Script is currently not working.  Getting error at make step of the script.  Potentially a path issue.

# Running pibeat

1. Copy pibeat to the Raspberry Pi (/home/pi)
2. Make pibeat executable
3. ```sudo chmod +x pibeat```
4. Run pibeat
5. sudo ./pibeat

# Configure Filebeat
1. Edit filebeat.yml.  Must be root 
2. ```sudo su```
3. ```sudo nano /etc/filebeat/filbeat.yml```
4. Configure the filebeat.yml to collect logs as needed for your logging preferences.
5. Enable modules needed for your preferences.
Filebeat [Documentation]()

# Setup Filebeat Service
1. ```sudo nano /lib/systemd/system/filebeat.service```
2. Enter the information exactly as it appears
```
[Unit]
Description=filebeat
Documentation=https://www.elastic.co/guide/en/beats/filebeat/current/index.html
Wants=userwork-online.target
After=network-online.target

[Service]
ExecStart=/usr/share/filebeat/bin/filebeat -c /etc/filebeat/filebeat.yml -path.home /usr/share/filebeat -path.config /etc/filebeat -path.data /var/lib/filebeat -path.logs /var/log/filebeat
Restart=always

[Install]
WantedBy=multi-user.target
```
3. Save the file and close
4. Enable the filebeat service
5. ```sudo systemctl enable filebeat.service```
6. This will create a symlink.  After step five you should see a return message
```Created symlink /etc/systemd/system/multi-user.target.wants/filebeat.service → /lib/systemd/system/filebeat.service.```
7. Start the filebeat service
8. ```sudo service filebeat start```
9. Check filebeat service status
10. ```sudo service filebeat status```

Note: Be sure to enable the module(s) you are using with filebeat.
Modules [Documentation](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-modules.html)

example: ```filebeat modules enable logstash```
