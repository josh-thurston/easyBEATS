When compiling the Beats modules for ARM, the files and services are not created and placed in the proper locations by default.

pibeat should place files in the correct locations and modify privileges automatically.  The information below is for reference.

Credit to 'Michael' for all his work published @ https://www.elasticice.net/?p=92

| Type | Description | Config Option | Default Location | Debian Default Path |
|------|-------------|---------------|------------------|---------------------|
| home | Home of Filebeat Installation | path.home | | /usr/share/filebeat |
| bin  | the location for the binary files | | (path.home)/bin | /usr/share/filebeat/bin |
| config | The location for configuration files | path.config | (path.home) | /etc/filebeat |
| data | The location for persistent data files | path.data | (path.home)/data | /var/lib/filebeat |
| logs | The location for the logs created by Filebeat | path.log | (path.home)/logs | /var/log/filebeat |

## The following directories will be created:

- ```/usr/share/filebeat``` 
- ```/usr/share/filebeat/bin```
- ```/etc/filebeat```
- ```/var/log/filebeat``` 
- ```/var/lib/filebeat```

## The following files will be Moved or Copied automatically:

- ```mv filebeat /usr/share/filebeat/bin```
- ```mv module /usr/share/filebeat/```
- ```mv modules.d/ /etc/filebeat/```
- ```cp filebeat.yml /etc/filebeat/```

## The following privilege changes will be made automatically:

- ```chmod 750 /var/log/filebeat```
- ```chmod 750 /etc/filebeat/```
- ```chown -R root:root /usr/share/filebeat/*```

## Configure filebeat

1. Edit ```/etc/filebeat/filebeat.yml``` to meet your needs.
2. Enable the modules that meet your needs.  This can be done in the filebeat.yml or manually
```filebeat modules enable osquery``` replace osquery with one ore more module names that you would like to run.

## Enable and Running Filebeat service

1. Enable the filebeat service that you just created

```sudo systemctl enable filebeat.service```

After enabling the service you should see a return message:

```Created symlink /etc/systemd/system/multi-user.target.wants/filebeat.service → /lib/systemd/system/filebeat.service.```

2. Start the filebeat service

```sudo service filebeat start```

3. Check status to make sure it is running

```sudo service filebeat status```

Service status should return a message:
```
● filebeat.service
   Loaded: loaded (/lib/systemd/system/filebeat.service; enabled; vendor preset: enabled)
   Active: active (running) since Sat 2019-09-28 20:17:36 BST; 18s ago
 Main PID: 31053 (filebeat)
    Tasks: 13 (limit: 4915)
   Memory: 5.4M
   CGroup: /system.slice/filebeat.service
           └─31053 /usr/share/filebeat/bin/filebeat -e -c /etc/filebeat/filebeat.yml

Sep 28 20:17:36 raspberrypi filebeat[31053]: 2019-09-28T20:17:36.483+0100        INFO        reg
```

4. To stop

```sudo service filebeat stop```

5. To restart

```sudo systemctl restart filebeat.service```

