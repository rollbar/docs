**Note:** The upgrade process currently requires stopping all Rollbar services before performing the upgrade. 
During this time, errors will not be captured. We will provide a zero-downtime upgrade process in 
a future release.

1. Download the new On-Premises distribution *.tar.gz* file
2. Uncompress and unarchive

   ```sh
   cd rollbar-enterprise_2016-03-01 && ./install.sh
   ```
3. Stop all Rollbar services
   
   If Rollbar is running on multiple hosts, perform this step on each host
   
   ```sh
   ./stop.sh
   ```
4. Install the new version

   ```sh
   ./install.sh
   ```
5. Configure using your previous settings

   The settings file from your previous install will be stored in the directory 
   you uncompressed the original archive into. Copy this file into the new distribution directory
   and name it ".settings".
   
   If you do not have this file it is likely that you are upgrading from a version built before 
   2/16/2016. See instructions below.
   
   ```sh
   ./configure.sh -f .settings --save
   ```
6. Start/upgrade to the new version

   ```sh
   ./start.sh --run-migrations
   ```
   
### FAQ

#### Q. Why am I seeing "sudo: unable to resolve host ..." when I run *configure.sh*?

See the answer [here](https://github.com/rollbar/docs/blob/master/on-premises/install.md#q-why-am-i-seeing-sudo-unable-to-resolve-host--when-i-run-configuresh).

### Upgrading from a version built before 2/16/2016

There are a couple of extra steps that a required in order to upgrade from a version build before
2/16/2016.

- The configure step will require some extra information for external services and the hostname
  
  If you are using any external services, (e.g. your own MySQL, Redis, Memcache, Beanstalk, Postfix server)
  you will need to provide these IPs to the configure script. 

  Also, you will need to specify the hostname for the Rollbar server. See the `--name` parameter.

  See `configure.sh -h` for more information on which parameters to use.

- Data directories will need to be moved into the new location

  Previous versions save data in */data/** but the newer version stores data in */opt/rollbar*. 
  In order to upgrade from one of these versions, you will need to rename the */data/** directories
  to */opt/rollbar/** before running *start.sh*.
  
  E.g.
  
  ```sh
  mkdir -p /opt/rollbar
  mv /data/* /opt/rollbar/
  ```

If you run into any trouble, please contact support@rollbar.com and we will get you set up quickly.
