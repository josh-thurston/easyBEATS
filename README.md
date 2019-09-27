# pibeat Setup Guide

At the time of creating this script, Elastic has not released an ARM version for Beats, so it is necessary to build a 
the Beats data shippers for arm architecture.  

pibeat will create:

- [Auditbeat](https://www.elastic.co/products/beats/auditbeat)
- [Filebeat](https://www.elastic.co/products/beats/filebeat)
- [Heartbeat](https://www.elastic.co/products/beats/heartbeat)
- [Metricbeat](https://www.elastic.co/products/beats/metricbeat)

Testing was performed on Raspberry Pi 3.+ and Raspberry Pi 4.  

System information for both is listed below with the commands to lookup the info on your system. If your system does not match
the following information, you may need to make some modifications.

**System Info**

```cat /etc/issue```
OS - Raspbian GNU/Linux 10
OS - Raspbian GNU/Linux 10 \n 1

```cat /etc/debian_version```
10.0
10.1

```python -V ```
Python 2.7.16

```python3 -V ```
Python 3.7.3

```git --version ```
git version 2.20.1

# Running pibeat

1. Copy pibeat to the Raspberry Pi (/home/pi)
2. Make pibeat executable
```chmod +x pibeat```
3. Run pibeat
``./pibeat``

After pibeat finishes, you will need to open up and edit some files

# Configure Beats Data Shippers

After creating the various data shippers (Auditbeat, Filebeat, Heartbeat, Metricbeat), the script places them in $HOME/beats.  Locate the shipper(s) you want to use and configure them as needed for your environment.

Example: Filebeat

1. Edit filebeat.yml. 
```nano $HOME/beats/filebeat/filbeat.yml```
2. Configure filebeat.yml
3. Enable modules needed for your preferences.

Reference Filebeat [Documentation](https://www.elastic.co/guide/en/beats/filebeat/current/configuring-howto-filebeat.html)
