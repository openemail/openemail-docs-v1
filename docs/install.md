!!! warning
    Make sure you've read ["Prepare Your System"](https://docs.openemail.io/prerequisite-system/) before proceeding!

You need to install `Docker` and `Docker Compose` to setup **openemail** for your domain.

This section will help you to learn how to install [Docker](https://docs.docker.com/engine/installation/linux/) and [Docker Compose](https://docs.docker.com/compose/install/).

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
sudo apt-get install apt-transport-https  ca-certificates curl  gnupg-agent software-properties-common
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
**Install docker-ce**

**1\.** Update the `apt` package index.
```
sudo apt-get update
```
**2\.** Install the latest version of Docker CE and containerd.
```
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
**3\.** Verify that Docker CE is installed correctly by running the hello-world image.
```
sudo docker run hello-world
```
This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

**4\.** You may need to enable the service
```
sudo systemctl enable docker.service
```
!!!Note
    If you are planing to use CentOS as your **openemai** docker host please follow the official [CentOS docker-ce Installation Guide](https://docs.docker.com/install/linux/docker-ce/centos/)

## Install Docker Compose on Linux systems

On Linux, you can download the Docker Compose binary from the [Compose repository release page on GitHub](https://github.com/docker/compose/releases). Follow the instructions from the link, which involve running the curl command in your terminal to download the binaries. These step by step instructions are also included below.

**1\.** Run this command to download the latest version of Docker Compose:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
**2\.** Apply executable permissions to the binary:

```
sudo chmod +x /usr/local/bin/docker-compose
```

!!! Note
    If the command docker-compose fails after installation, check your path. You can also create a symbolic link to /usr/bin or any other directory in your path.

    For example:
    ```
    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
    ```

**3\.** Test your installation
```
docker-compose --version
```
## Cloning openemail repository

Clone the master branch of the repository, make sure your `umask` equals 0022.
```
sudo su -
umask
cd /opt
git clone https://github.com/openemail/openemail.git
cd openemail


```
## Generating openemail.conf

Generate a configuration file. Use a FQDN (`host.domain.tld`) as hostname when asked.

```
./generate_config.sh
```
## Customize the configuration

Change configuration if you want or need to.
```
nano openemail.conf
```
If you plan to use a reverse proxy, you can, for example, bind HTTPS to 127.0.0.1 on port 8443 and HTTP to 127.0.0.1 on port 8080.

You may need to stop an existing pre-installed MTA which blocks port 25/tcp. See [this chapter](https://docs.openemail.io/firststeps-local_mta/) to learn how to reconfigure Postfix to run besides mailcow after a successful installation.

## Setup MTU

OpenStack users and users with a MTU not equal to 1500:

Edit `docker-compose.yml` and change the network settings according to your MTU.
Add the new driver_opts parameter like this:

```
networks:
  openemail-network:
    ...
    driver_opts:
      com.docker.network.driver.mtu: 1450
    ...
```
## Pull openemail docker images

Pull the images and run the composer file. The parameter `-d` will start openemail docker containers detached:
```
docker-compose pull
docker-compose up -d
```
## Accessing openemail UI

You can now access **https://${OPENEMAIL_HOSTNAME}** with the default credentials `admin` + password `openemail`.

The database will be initialized right after a connection to MySQL can be established.

Done!
