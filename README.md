# heavyai-devstack

### Introducing heavyai-devstack 2.0.  The Next Generation !

This latest generation of the devstack config has been redesigned to support some more robust installation options.  The most common usage of this will be for a simple docker container install on an Ubuntu22.04 host OS.  It has been tested on a few different architectures, but it may not be completely bullet proof.

There are two key components:

1. `checkEnv.sh` - this script checks for and optionally adds needed packages to the environment to provide the correct foundation.  This will check and optionally install and configure:  
 -Docker components (docker.io or docker-ce and docker-compose ).  Either of these packages will work, but one of them must exist.  
 -xmlstartlet.  This component is a convenience for these scripts to leverage  
 -nvidia drivers  
 -nvidia runtime container  
 -awscli - This is optional, but often helpful


 In general, if the script finds missing components, it will prompt to install them

NOTE:  I have found that if you need to install Nvidia drivers, you must reboot the machine after driver install and before Nvidia Toolkit / Docker Runtime install.

2. `configureHeavy` - this script will generall take the template files from the templates folder and modify them with the appropriate values specified in the top of the script.  These config files will use be copied, updated with values, and then moved to the appropriate config file location.  If desired, the values of some most of the variables in this file can also be set in a `.env` file instead of in the script itself.

This script can take an optional parameter `configureHeavy -soa`.  This will create a more complex deployment that puts heavydb, immerse, and heavyiq each in it's own container.  It will create separate config files for each component, and an appropriate docker-compose.yml file to start all of the services.  This is an advance configuration option.

Once the two scripts above have run successfully, there will be a `docker-compose.yml` file in the user's home directory that can be used to launch the container(s).  You can simply execute:

`docker compose up -d`

To monitor the process of startup, you can use the command:

`docker compose logs -f`

If you want to stop a service or all of the services you should use:

`docker compose stop`
