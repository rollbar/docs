The upgrade process currently requires stopping all Rollbar services before performing the upgrade. 
During this time, errors will not be captured. We will provide a zero-downtime upgrade process in 
a future release.

1. Download the new On-Premise distribution *.tar.gz* file
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
   you uncompressed the original archive into.
   
   ```sh
   ./configure.sh -f ../PREVIOUS_INSTALLATION_DIRECTORY/.settings --save
   ```
6. Start/upgrade to the new version

   ```sh
   ./start.sh --run-migrations
   ```
