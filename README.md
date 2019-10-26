# easyBEATS

easyBEATS is a project started to make the installation of Beats packages faster and easier for Ubuntu, Mac, and even Raspberry Pi (ARM architecture)

## How To Use

### beats_arm

Elastic.co has not released any of the Beats shippers for ARM architecture.  The beats_arm installer will download source code, compile an arm version, and prep the system for use.  The installer will prepare Filebeat, Packetbet, Metricbeat, and Auditbeat for use.  There are some TODO items as well as some quirks that I have noticed and not been able to solve yet. I have those TODO items and quirks noted below.  

1. Download beats_arm.zip and extract the contents
2. Copy beats_arm to your system
3. Inside beats_arm you will find an easyBEATS-7.3.2_arm install script
4. You need to make it executable and run it

```
sudo chmod +x easyBEATS-7.3.2_arm
./easyBEATS-7.3.2_arm
```

5. After the sccript is finished, configure each of the Beats shippers
    - /etc/filebeat/filebeat.yml
    - /etc/metricbeat/metricbeat.yml
    - /etc/packetbeat/packetbeat.yml
    - /etc/auditbeat/auditbeat.yml
6. The script has already prepared the system to launch the service at boot / re-boot.  You just need to start the service after you configure

```
sudo systemctl start filebeat metricbeat packetbeat auditbeat
```

7. Run the setup command for each to finalize

```
sudo /usr/share/filebeat/bin/filebeat setup -e -c /etc/filebeat/filebeat.yml
```

Repeat the command and change the name of filebeat to each of the other beats

**Quirks:**

1. I am unable to get the Path working correctly for the beats products.  Some normal command either dont work or you must use a workaround.  an example of a workaround is in the previous step to launch setup.  A normal setup on a system such as Ubunut, you just type "filebeat setup -e" and it will work.  
2. Some of the beats products use 'modules' to extend functionality.  Typically you can type something similar to "filebeat modules enable osquery" to enable and use the module. I have not been able to get that command to work.  To use the modules, you will need to configure the module inside the configuration file. 
    - [filebeat example](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-modules.html)

**TODO:**

1. Need to work on the Auditbeat script.  Getting Auditbeat to function on arm has been inconsistent in testing with Raspberry Pi 3b+ and Raspberry Pi 4.  Getting erros on supported architecture that need resolved.
2. Need to fix the Path issue noted in the Quirks section.

### Debian (Ubuntu)

easyBEATS-7.3.2_deb will install Filebeat, Metricbeat, Packetbeat, and Auditbeat.  It *Does Not* use apt-get and the script puts each of the beats packages on apt-get hold to prevent accidental upgrading.  If you want to upgrade you must remove the hold.  I do this to avoid accidentally upgrading my beats clients to a newer version that my ELK stack.

1. Download easyBEATS-7.3.2_deb 
2. Copy to your debian system
3. Make it executable and run it

```
sudo chmod +x easyBEATS-7.3.2_deb
./easyBEATS-7.3.2_deb
```

4. After the sccript is finished, configure each of the Beats shippers
    - /etc/filebeat/filebeat.yml
    - /etc/metricbeat/metricbeat.yml
    - /etc/packetbeat/packetbeat.yml
    - /etc/auditbeat/auditbeat.yml
5. The script has already prepared the system to launch the service at boot / re-boot.  You just need to start the service after you configure

```
sudo systemctl start filebeat metricbeat packetbeat auditbeat
```

7. Run the setup command for each to finalize

```
filebeat setup -e
```

Repeat the command and change the name of filebeat to each of the other beats

**TODO:**

Finalizing the script for easyBEATS-7.4.1_deb

### Mac

easyBEATS_mac will install Filebeat, Metricbeat, Packetbeat, and Auditbeat using Homebrew. It will install whatever the latest version is availabe from Homebrew.  If your Mac does not have Homebrew installed, the script will install it for you.

**Note:** The directory layout for Mac is slightly different than other installations.  You can find reference [elastic here](https://www.elastic.co/guide/en/beats/filebeat/current/directory-layout.html) for a listing of the directory layout by system type.  

1. Download easyBEATS_mac 
2. Copy to your Mac system
3. Make it executable and run it

```
sudo chmod +x easyBEATS_mac
./easyBEATS_mac
```

4. After the sccript is finished, configure each of the Beats shippers
    - /usr/local/etc/filebeat/filebeat.yml
    - /usr/local/etc/metricbeat/metricbeat.yml
    - /usr/local/etc/packetbeat/packetbeat.yml
    - usr/local/etc/auditbeat/auditbeat.yml

```
brew services start elastic/tap/filebeat-full
```

7. Run the setup command for each to finalize

```
filebeat -e
```

Repeat the command and change the name of filebeat to each of the other beats

### Remove / Uninstall

If you mess up or you want to remove everything you can run removeBEATS-7.3.2 on arm and deb, or removeBEATS_mac for Mac OS X. 

## Additional Info

Check out [Beats](https://www.elastic.co/products/beats) and prepare data shippers.
