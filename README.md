# easyBEATS

### Credit where credit is due

easyBEATS is a project started by josh-thurston to make the installation of Beats packages faster and easier for Ubuntu, Mac, and even Raspberry Pi (ARM architecture).

### About this fork

My fork is focused entirely on Raspberry Pi.  It resolves issues related to the outdated golang-go package in the RPi apt repo which prevents the successful installation of Beats newer than v7.3.2.  I've refactored the script such that you can install one or multiple Beats at any version.

The instructions are here so that you can compile Beats on your own.  If you would prefer something a bit easier that doesn't require compiling source code, visit my [Beats-Pi repo](https://github.com/RaoulDuke-Esq/Beats-Pi) for some pre-baked Beats that you can install via apt.

## How To Use

### Clone the repo
Clone the repo to your home directory.

```
cd ~
git clone https://github.com/RaoulDuke-Esq/easyBEATS.git
cd easyBEATS
```

Now make the install script executable.

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
BEAT_NAME=( metricbeat filebeat ) #metricbeat filebeat packetbeat auditbeat journalbeat heartbeat
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
I have only tested metricbeat, packetbeat, and filebeat.  Your mileage may vary on the others.  

File an issue if you run into a problem or have a question.  I'm happy to help!



## Additional Info

Check out [Beats](https://www.elastic.co/products/beats) to learn more.
