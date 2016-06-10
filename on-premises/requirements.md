# Configuration Requirements for Rollbar On-Premises

## Hardware

The single-host install should work well with the following specs.  This
is the equivalent an AWS EC2 m4.xlarge instance.

- 4+ core
- 16GB RAM
- 100+GB disk

## Operating System and Packages

Currently we've only verified our on-premises product to work on the
following, though we're working on adding more Linux operating system
distributions and versions.  Due to the fact that we're running on
Docker, this will never run natively on Windows or Mac hosts.  You'll
have to setup some sort of virtual machine(s) in those instances.

- Ubuntu 14.04 LTS
- Docker v1.9.1+
  - Tested with Docker 1.9.1, 1.10.1
- Docker Compose 1.6.1

## Email

In some of the environments we've encountered, the built-in SMTP server
has problems sending mail.  Generally this is from things like bad IP
address reputation or lack of good SPF and DKIM setups.  Needless to
say, you'll almost certainly want to run your own SMTP server, or hook
in to a service like Mailgun or Amazon SES.

## Network Configuration

We assume that you will at least have a publicly facing network and a
private network for the docker host or hosts (if not more).  The
following ports need to be open, both on the public and private
networks:

* outbound ports: 25 (smtp), 80 (http) && 443 (https)
* inbound ports: 80 (http) && 443 (https)

If you're running some of the base services yourself instead of using
the Rollbar supplied docker instances, you'll need to make sure all the
necessary ports are open on your private network to talk to these
services.  You won't want to expose these ports publicly unless you are
*VERY* sure that you've got all your security ducks in a row (and you
almost certainly don't).  We expect each service to be running on its
default port, since we give you a way to specify IP addresses for these
services, but not ports:

* mysql - 3306
* memcached - 11211
* redis - 6379
* beanstalk - 11300
* sphinx - 9306

If you're running Rollbar on multiple hosts, you'll need to make sure
the following ports are open on your private network for the services on
each host to talk to each other. Do *NOT* open these ports on your
public network because we did not design these services to be publicly
facing and there isn't any encryption or authentication between them,
which is very dangerous on the open internet.

* moxui - 8080
* react renderer - 8081
* mox rts - 8082
* search api - 8083
* haproxy stats url - 8999
