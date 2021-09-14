# easyBEATS


### About

easyBEATS is a project started to make the installation of Beats packages faster and easier for Ubuntu, Mac, and even Raspberry Pi (ARM architecture). The focus was for Rasperry Pi since Elastic does not have a supported release on ARM architecture.  easyBEATS also resolves issues related to the outdated golang-go package in the RPi apt repo which prevents the successful installation of Beats newer than v7.3.2.  The current version of the script will let you install one or multiple Beats at any version.

## Export

The **export branch** changes the default behaviour to export beat installation files. There are a couple parameters added:

```
EXPORT_DIR="beat-export" #this directory will be created in /home/pi
EXPORT_INSTALL=true #set to false if you do not want to export
```

### Default

The default values are set according CI purposes.

```
UPDATE_SYSTEM=true
INSTALL_DEPS=true
USE_SWAP=false
WORKING_DIR="beat-factory"
BEAT_VERSION="v7.11.0"
BEAT_NAME=( metricbeat )
INSTALL_LOCAL=true
CLEAN_UP=true
EXPORT_DIR="beat-export"
EXPORT_INSTALL=true
```

## How To Use

### Clone the repo

Install git on your Pi so you can clone from this GitHub repo.

```
sudo apt-get install git -y
```

Clone the repo to your home directory.


Now make the install script executable so you can run it.

```
sudo chmod 755 easyBEATS
```

### Configure the script
There are a few variables we need to define.  Open the script with a text editor.

```
vi easyBEATS
```

Review the default options at the top of the script and change as necessary.

```
UPDATE_SYSTEM=true #change to false if you don't want to upgrade your whole system
INSTALL_DEPS=true #change to false if you have already run this script successfully before
USE_SWAP=true #change to fales if you're using a Pi4 with 2GB of RAM or more
WORKING_DIR="beat-factory" #this directory will be created in /home/pi
#visit https://github.com/elastic/beats/releases to find other version numbers and commit numbers
BEAT_VERSION_NUM="7.5.2" #the version number of the Beats release you want to use
BEAT_VERSION="a9c1414" #the commit number of the Beats release you want to use
#add as many beats as you want to BEAT_NAME separated by a space
BEAT_NAME=( metricbeat filebeat ) #metricbeat filebeat packetbeat auditbeat heartbeat
INSTALL_LOCAL=true #set to false if you only want to compile without installing
CLEAN_UP=true #set to false if you want to keep the source files on your Pi
```

Save your changes and quit VI by typing Esc ZZ.

### Run the script

```
./easyBEATS
```

### Configure your Beats and start them up.

After the script is finished, configure each of the Beats shippers.  Configuration files are found in /etc/$BEAT_NAME

```
#filebeat example
cd /etc/filebeat
sudo vi filebeat.yml
```

For guidance on how to configure, visit [Elastic's documentation](https://www.elastic.co/guide/) and check out the section for Beats.  Some of the Beats have modules.  Enable these by renaming them.

```
cd /etc/filebeat/modules.d
ls
mv system.yml.disabled system.yml
```

The script has already prepared the system to launch the service at boot / re-boot.  You just need to start the service after you configure

```
#filebeat example
sudo systemctl start filebeat.service
```

### Remove / Uninstall

If you mess up or you want to remove everything you can run removeBEATS.


## Notes
Tested with metricbeat, packetbeat, and filebeat.  Others may work but have not been tested.  

File an issue if you run into a problem or have a question.



## Additional Info

Check out [Beats](https://www.elastic.co/products/beats) to learn more.
