Tyk Host Manager
================

The Tyk Host manager is a small daemon that will listen to your Tyk Redis cluster for API changes and then hot-reload any Tyk processes you have running on the system.
THis is the best way to have the tyk Dashboard manage your cluster, naturally manual restarts can also be run.

The Host Manager only works with a MongoDB-backed Tyk setup, as the Tyk instances will need to access live change data and this will only work via the Mongo storage method.

## Setup

Tyk Host manager can also manage your NGinX setup by creating new entries in your sites-available folder for each API that is active on the system. This is covered later
in this document.

Tyk host Manager is configured using a file called host_manager.json, this is a standard JSON file that should have come with this tarball, if it does not exist
it looks like this:

    {
        "mongo_url": "mongodb://username:password@mongohost.com:PORT/db_name",
        "redis_port": 6379,
        "redis_host": "localhost",
        "redis_password": "test",
        "tyk_ports": [5000],
        "tyk_secret": "352d20ee67be67f6340b4c0605b044b7",
        "license_owner": "Your Name"
    }
    
To get started:

1. Set up the correct Mongo and Redis details in the `mongo_url` and `redis_*` fields, these are pretty self explanatory and should match what you have in your tyk instance configuration
2. The host manager assumes it is on the same host as your tyk processes, enumerate their port numbers in the `tyk_ports` section
3. Set the `tyk_secret` field to tbe the same as that in your tyk instance configuration
4. Set the license owner tobe the same as that emailed to you by the license service

If all the details are coorect, you should be able to start the tyk host service y running:

    martin@vyr > ./tyk-host-manager


## Working with NGinX

The tyk host manager can create and update NginX server entries for your APIs, this makes it easy to set up redirects for your services against sub-domains without
having to map them manually - i.e. you create a new API that listens on /my-api, and the host mnager will create an entry for NginX (based on a template) that 
would be: my-api.tyk.io, which then redirects the root URL to the `listen_path` of your new API setup.

To get this up and running the quickest way is:

1. Ensure that the `nginx_confs` folder is symlinked to `etc/nginx/sites-available`
2. Ensure that you are using (or have incorporated) the `configurations/nginx.conf` configuration file into your production version
3. Modify the `templates/nginx.conf` to suit your site setup, the available variables are demarkated as `{{ .X }}` and are inserted by Golang, no additional varibales are available except those listed in the example template

Note, for NginX implementations, this application must be run as sudo, otherwise nginx will not reload. Secondly, NginX is restarted using a 
service command, so please ensure that running `sudo service nginx restart` works first.



