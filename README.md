# Nutanix Graphical API Demos v2 (Laravel)

Demo app aimed at showing how to consume the Nutanix v2 REST API using PHP.

# Changelog

- 2021.05.06 - ChrisRNutanix - Moved from `nutanix/automation` to `nutanixdev/graphical-api-demo`
- 2021.05.06 - ChrisRNutanix - Embedded Cloud-Init data vs requirement for cluster-hosted .yaml file
- 2018.04.24 - ChrisRNutanix - Updated with detailed setup instructions

# Requirements

- PHP >=5.5.9
- MySQL server as per standard Laravel app requirements (local or remote - doesn't matter as long as the web server can access)

# Requirements - Full VM Deployment

- For reference only, the `web-server.yaml` in this repo
- An existing CentOS Linux VM that has the `cloud-init` package **already installed** (this is critical)
- To make parameter entry easy, you can click 'Need cluster details? Click here!' then 'Get Details'.  Click the container name you want to use, the network UUID you want to use and the disk UUID you want to use.  Please note the selected disk UUID must be one that has `cloud-init` already installed

The "Full VM Deployment" with Cloud-Init will also install the `httpd` web server.  After deployment, the deployed VM's default web server pages can be accessed on the VM's primary IP address.

## Detailed Installation Steps (OS X & Linux)

- Ensure [PHP Composer](https://getcomposer.org) is available on the target web server
- Ensure MySQL is available, including credentials to access it _remotely_
- Clone repo from this location
- Install Composer dependencies:

  ```
  composer install
  ```

- Run Composer update, to make sure packages are latest (not really required, but you never know)

  ```
  composer update
  ```

- Rename `.env.example` to `.env`
- Edit the `.env` file, paying particularly attention to the MySQL database connection parameters
- Generate the Laravel application key:

  ```
  php artisan key:generate
  ```

- Run the database migrations and make sure no database-related errors are shown during this step:

  ```
  php artisan migrate
  ```

- Seed the database and make sure no database-related errors are shown during this step:

  ```
  php artisan db:seed
  ```

- The application's `storage` directory needs to be world-writable (used for caching and temporary logs).  Do this now, from the downloaded repo's root directory:

  ```
  chmod -R 0777 ./storage
  ```

- Run the demo using local PHP development server (recommended):

  ```
  php artisan serve
  ```

  Note: Deployment of a Laravel PHP application on Nginx or Apache (etc) is beyond the scope of this demo.

- Browse to `http://localhost:8000`
- Login with username `no-reply@acme.com` and password `password`
- Enter cluster details:

  - Cluster virtual IP or CVM IP address (this **must** be the cluster IP or CVM IP, **not** Prism Central)
  - Username
  - Password
  
- Select the required demo from Step 2
- Click 'Run Demo'
- Check out the results in Step 3
- After deployment, the deployed VM can be accessed via SSH with username `nutanix` and password `nutanix/4u`

# Note
moved to /nutanix/automation from https://github.com/digitalformula/nutanix-graphical-api-demo-2 (JonKohler 2018.04.06)