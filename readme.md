# cms
## Setup
- download/clone the git repository from
  - `git clone https://github.com/karlkras/cms.git`
- navigate into the project folder
  - `cd cms`
- make sure not to work directly on the master branch  
  - `git checkout -b my_local_branch`
- to prepare the vagrant configuration, run
  - `vendor/bin/homestead make` or `vendor/bin/homestead.bat make` on Windows
- adjust the `hosts` file and the newly created `Homestead.yaml` in the root of the repo according to your needs. Usually that includes:
  - adjust `ip`
    - make sure the `ip` is not already used in your local network
  - add a couple of entries to your host file
    - `[IP] cms.test` (e.g. `192.168.33.111 cms.tet`)
    - `[IP] phpmyadmin.test` (e.g. `192.168.33.111 phpmyadmin.test`)
    - location on Unix: `/etc/hosts`
    - location on Windows: `C:\Windows\System32\drivers\etc`
- adjust `folders` and `sites` mapping (optional; it should be set up correctly by default if you followed the steps above).
  Watch out for the following:
  - the `folders: - map: "[PATH]"` should point to the absolute path to the `cube` repository on your **local** machine
  - the `folders: to: "[PATH]"` denotes the path on your **vagrant** machine that is mapped to the above mentioned path on your local machine,
    so that you can access your local files within the vagrant box.
  - the `sites: - map: "[HOSTNAME]"` denotes the hostname that the nginx is looking for to serve content on
    - you _should_ adjust that to the hostname chosen for your hostfile (e.g. `laravelexample.app`) although it not necessary since nginx will even respond to another hostname
  - the `sites: - to: "[PATH]"` denotes the absolute path withing the vagrant box that the above mentioned hostname uses as `root` path for content.
    This should be the path to the `public` folder of this repository
- start the vagrant box with `vagrant up`, ssh into it with `vagrant ssh`, switch to the project folder (by default, this should be `cd /home/vagrant/laravelexample/`) and install the 
  project's dependencies
  - `composer install`
- setup laravel by generating an application key and setting up the .env file:
  - php artisan key:generate
  - `cp .env.example .env`
- generate the meta data files for better code completion
  - `php artisan ide-helper:meta`
  - `php artisan ide-helper:generate`
  - `php artisan ide-helper:model`

You should now be able to open http://cms.test/ and http://phpmyadmin.test/ in your browser and see the Laravel welcome page :)