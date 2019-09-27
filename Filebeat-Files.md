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

## Create the following:

- ```/usr/share/filebeat``` 
- ```/usr/share/filebeat/bin```
- ```/etc/filebeat```
- ```/var/log/filebeat``` 
- ```/var/lib/filebeat```

## Move / Copy the following files:

- ```mv filebeat /usr/share/filebeat/bin```
- ```mv module /usr/share/filebeat/```
- ```mv modules.d/ /etc/filebeat/```
- ```cp filebeat.yml /etc/filebeat/```

## Edit Privileges

- ```chmod 750 /var/log/filebeat```
- ```chmod 750 /etc/filebeat/```
- ```chown -R root:root /usr/share/filebeat/*```
