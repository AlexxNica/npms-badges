# Deploys

We use `pm2` to deploy `npms-badges`, install it by running `$ npm install -g pm2`. You may find the pm2 configuration file in `ecosystem.json5`.


## Setting up

Before doing the first deploy, you need to setup the server. All commands executed in the server are expected to be run with the `www` user.

- Create the `www` user on server
- Add `www` user to the list of sudoers
- Install pm2 in the server
- Setup the deploy environment by running `$ pm2 deploy ecosystem.json5 production setup` in your local machine
- Create `~/npms-badges/local.json5` in the server with the custom configuration (elasticsearch host, etc)
- Do your first deploy by running `$ pm2 deploy ecosystem.json5 production` in your local machine
- Setup logrotate by running `$ sudo pm2 logrotate -u www` on the server and then edit `/etc/logrotate.d/pm2-www` to change change `/root` to `/home/www`, weekly to daily, and from 12 days to 14 days)
- Setup pm2 to run at start by running `$ sudo pm2 startup -u www --hp "/home/www"` on the server
- Finally run `$ pm2 save` to store the running processes


## Deploying

Deployment is easy, just run `$ pm2 deploy ecosystem.json5 production` in your local machine
