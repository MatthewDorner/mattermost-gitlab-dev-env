# Mattermost GitLab Dev Environment #

Docker scripts for spinning up a GitLab instance and Nginx SSL reverse proxy for testing and developing on the Mattermost GitLab plugin.

- Runs an instance of GitLab Omnibus EE in Docker
- Runs Nginx reverse proxy in docker to serve SSL certificates and deliver traffic to either the GitLab instance or the Mattermost server on `:8065`
- Uses a public IP, DNS and SSL for realistic testing of webhook, SSL, OAuth issues.
- Services are made available as `https://mattermost.example.com` and `https://gitlab.example.com`

## Setup ##
I set this up to use a real public IP, DNS and SSL. You could modify it if you want to work differently but I hard a hard time getting SSL to work with self-signed local certs. You'd use a wildcard in your DNS record and then both services are on a single IP and Nginx sorts traffic to the two services based on the subdomain. Insert the `certificate.crt` and `key.key` in `./proxy/ssl` folder. Replace references to `"mattermost.example.com"` and `"gitlab.example.com"` in `./proxy/default.conf` and `./docker-compose.yml` with your own domain. Of course I had to add port forwarding to my router for 80 and 443 and you might want to change those default passwords if you set it up this way.

## Use ##
Just run Mattermost dev server normally on `:8065` and run `docker-compose up` in this repo to launch Nginx and GitLab.

The GitLab instance will create a password for the `root` user at `./gitlab/config/initial_root_password` the first time you run it.