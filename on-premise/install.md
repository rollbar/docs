# Setup

## Docker and Docker Compose

Full Docker installation instructions for Ubuntu: https://docs.docker.com/engine/installation/linux/ubuntulinux/

Here's a cheat sheet to download and install Docker Engine on Ubuntu 14.04 LTS:

```sh
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates
sudo sh -c 'echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" > /etc/apt/sources.list.d/docker.list'
sudo apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
sudo apt-get update
sudo apt-get purge lxc-docker
sudo apt-cache policy docker-engine
sudo apt-get install linux-image-extra-$(uname -r)
sudo apt-get install docker-engine
sudo service docker stop
sudo service docker start
```

To make docker work without requiring sudo:

```sh
sudo usermod -aG docker ubuntu
# then log out and log back in
```

Full Docker Compose installation instructions: https://docs.docker.com/compose/install/

Here's a cheat sheet to install the required version of Docker Compose:

```sh
sudo sh -c 'curl -L https://github.com/docker/compose/releases/download/1.6.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose'
chmod +x /usr/local/bin/docker-compose
```

# Single host

1. Download the on-premise distribution .tar.gz file
   - Example: *rollbar-enterprise_2016-02-12.tar.gz*
2. Uncompress and unarchive

    ```sh
    tar -xzf rollbar-enterprise_2016-02-12.tar.gz
    ```
3. Install

    ```sh
    cd rollbar-enterprise_2016-02-12 && ./install.sh
    ```
4. Configure

    ```sh
    ./configure.sh -n rollbar.mycompany.com --save
    ```
5. Start

    ```sh
    ./start.sh --run-migrations
    ```
6. Navigate your browser to https://rollbar.mycompany.com/

# Multiple Hosts

Before you read this, take a moment to familiarize yourself with the
[Rollbar On-Premise architecture](architecture.md "Rollbar On-Premise Architecture") and
the [advanced configuration](configure.md#advanced "Advanced Rollbar Configuration")
documentation.

You can install Rollbar on one or more hosts. Before you start, you will need to determine
which services you want to run on the extra hosts. Below are some common choices:

- Run your MySQL database on a separate, dedicated host
  - Run your own managed MySQL database - See the [Advanced Configuration](configure.md#advanced "Advanced Rollbar Configuration") instructions.
  - Run the bundled MySQL database that came with the On-Premise distribution
- Run extra Rollbar data pipeline workers
- Add capacity to the Rollbar API tier by adding more API servers
- Add capacity to the Rollbar Web tier by running more Web servers

For a full list of the different services you can install and run, see the
[configuration](configure.md "Rollbar Configuration") documentation.

## Requirements

- Download and unarchive the *.tar.gz* file onto your hosts
- The *.settings* file from your original Rollbar host copied onto your other hosts in the same
  directory as the *configure.sh* script.

## Configure

Next, run the *configuration.sh* script on your new hosts but this time, specify which services
you would like to install and run.

### Run the bundled MySQL database

```sh
./configure.sh -f .settings --services mysql --save
```

### Run extra Rollbar workers

```sh
./configure.sh -f .settings --services worker --save
```

### Add capacity to the Rollbar API/Web tier

```sh
./configure.sh -f .settings --services api,web --save
```

### FAQ

#### Q. Why am I seeing "sudo: unable to resolve host ..." when I run *configure.sh*?

Depending on your host configuration, it's possible that your hostname cannot be resolved.
The quickest fix is to add your hostname to */etc/hosts*.

E.g.
```
echo "127.0.1.1 $(hostname)" >> /etc/hosts
```

#### Q. My email doesn't seem to be sending.  What's up with that?

Take a look at our [email page](email.md).
