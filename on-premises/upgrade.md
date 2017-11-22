**Note:** The upgrade process currently requires stopping all Rollbar
services before performing the upgrade.  During this time, errors will
not be captured. We will provide a zero-downtime upgrade process in a
future release.

1. Download the new On-Premises distribution `.tar.gz` file
2. Uncompress and unarchive (file and directory names will change with
   the release version)

   ```sh
   tar -xzvf rollbar-enterprise_0.8.4.tar.gz
   cd rollbar-enterprise_0.8.4
   ```
3. Stop all Rollbar services

   If Rollbar is running on multiple hosts, perform this step on each
   host

   ```sh
   ./stop.sh
   ```
4. Install the new version

   ```sh
   ./install.sh
   ```
5. Configure using your previous settings

   5a. Copy your old `.settings` file into the current directory
   
   ```sh
   cp /path/to/old/version/.settings .
   ```
   
   5b. Run configure

   ```sh
   ./configure.sh -f .settings --save
   ```
   
6. Start/upgrade to the new version

   ```sh
   ./start.sh --run-migrations
   ```

7. Initialize ElasticSearch

   We've changed from using Sphinx as our search engine to
   ElasticSearch.  As a result of this, you'll need to initialize
   ElasticSearch before search will work in your application.

   ```sh
   ./utils.sh --es-init --es-index
   ```

### FAQ

#### Q. Why am I seeing `sudo: unable to resolve host ...` when I run `configure.sh`?

See the answer
[here](https://github.com/rollbar/docs/blob/master/on-premises/install.md#q-why-am-i-seeing-sudo-unable-to-resolve-host--when-i-run-configuresh).

### Upgrading from a version built before 2/16/2016

There are a couple of extra steps that are required in order to upgrade
from a version build before 2/16/2016.

- The configure step will require some extra information for external
  services and the hostname

  If you are using any external services, (e.g. your own MySQL, Redis,
  Memcache, Beanstalk, Postfix server) you will need to provide these
  IPs to the configure script.

  Also, you will need to specify the hostname for the Rollbar
  server. See the `--name` parameter.

  See `configure.sh -h` for more information on which parameters to use.

- Data directories will need to be moved into the new location

  Previous versions save data in `/data/*` but the newer version stores
  data in `/opt/rollbar`.  In order to upgrade from one of these
  versions, you will need to rename the `/data/*` directories to
  `/opt/rollbar/*` before running `start.sh`.

  E.g.

  ```sh
  mkdir -p /opt/rollbar
  mv /data/* /opt/rollbar/
  ```

If you run into any trouble, please contact support@rollbar.com and we
will get you set up quickly.
