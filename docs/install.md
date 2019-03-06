!!! warning
    Make sure you've read ["Prepare Your System"](https://docs.openemail.io/prerequisite-system/) before proceeding!

You need to install Docker and Docker Compose to setup **openemail** for your domain.

**1\.** Learn how to install [Docker](https://docs.docker.com/engine/installation/linux/) and [Docker Compose](https://docs.docker.com/compose/install/).

## Installing Docker Community Edition on Ubuntu

To install Docker CE, you need the 64-bit version of one of these Ubuntu versions:

- Cosmic 18.10
- Bionic 18.04 (LTS)
- Xenial 16.04 (LTS)

In this guide I am using Bionic 18.04 (LTS)

**Uninstall old versions**

Older versions of Docker were called `docker, docker.io , or docker-engine.` If these are installed, uninstall them:
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```
**Install using the repository**

Before you install Docker CE for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

**Setup the repository**

**1\.** Update the apt package index:
```
sudo apt-get update
```
**2\.** install packages to allow apt to use a repository over HTTPS:
```
$ sudo apt-get install apt-transport-https  ca-certificates curl  gnupg-agent software-properties-common
```
**3.** Add Docker’s official GPG key:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88, by searching for the last 8 characters of the fingerprint.
```
sudo apt-key fingerprint 0EBFCD88
```
You should get an output like below.
```
pub   rsa4096 2017-02-22 [SCEA]
      9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid           [ unknown] Docker Release (CE deb) <docker@docker.com>
sub   rsa4096 2017-02-22 [S]
```
**4\.** Use the following command to set up the stable repository.
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```




- Docker
```
curl -sSL https://get.docker.com/ | CHANNEL=stable sh
# After the installation process is finished, you may need to enable the service and make sure it is started (e.g. CentOS 7)
systemctl enable docker.service
systemctl start docker.service
```

- Docker-Compose
```
curl -L https://github.com/docker/compose/releases/download/$(curl -Ls https://www.servercow.de/docker-compose/latest.php)/docker-compose-$(uname -s)-$(uname -m) > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

Please use the latest Docker engine available and do not use the engine that ships with your distros repository.

**2\.** Clone the master branch of the repository, make sure your umask equals 0022.
```
# umask
0022
# cd /opt
# git clone https://github.com/mailcow/mailcow-dockerized
# cd mailcow-dockerized
```

**3\.** Generate a configuration file. Use a FQDN (`host.domain.tld`) as hostname when asked.
```
./generate_config.sh
```

**4\.** Change configuration if you want or need to.
```
nano mailcow.conf
```
If you plan to use a reverse proxy, you can, for example, bind HTTPS to 127.0.0.1 on port 8443 and HTTP to 127.0.0.1 on port 8080.

You may need to stop an existing pre-installed MTA which blocks port 25/tcp. See [this chapter](https://mailcow.github.io/mailcow-dockerized-docs/firststeps-local_mta/) to learn how to reconfigure Postfix to run besides mailcow after a successful installation.

**4\.1\.** OpenStack users and users with a MTU not equal to 1500:

Edit `docker-compose.yml` and change the network settings according to your MTU.
Add the new driver_opts parameter like this:
```
networks:
  mailcow-network:
    ...
    driver_opts:
      com.docker.network.driver.mtu: 1450
    ...
```

**5\.** Pull the images and run the composer file. The parameter `-d` will start mailcow: dockerized detached:
```
docker-compose pull
docker-compose up -d
```

Done!

You can now access **https://${MAILCOW_HOSTNAME}** with the default credentials `admin` + password `moohoo`.

The database will be initialized right after a connection to MySQL can be established.
