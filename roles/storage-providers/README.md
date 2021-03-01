<p align="center"><img src="img/storage-provider_new.svg"></p>

<div align="center">
  <h4>This is a guide to setting up your <a href="https://github.com/Joystream/joystream/tree/master/storage-node">storage node</a>, and getting started as a Storage Provider on the latest
    <a href="https://testnet.joystream.org/">testnet</a>.</h4><br>
</div>



Table of Contents
==
<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
- [Overview](#overview)
- [Instructions](#instructions)
  - [Initial setup](#initial-setup)
  - [Install IPFS](#install-ipfs)
    - [Configure IPFS](#configure-ipfs)
    - [Run IPFS as a service](#run-ipfs-as-a-service)
  - [Setup Hosting](#setup-hosting)
    - [Instructions](#instructions-1)
    - [Run caddy as a service](#run-caddy-as-a-service)
  - [Install and Setup the Storage Node](#install-and-setup-the-storage-node)
  - [Update Your Storage Node](#update-your-storage-node)
    - [Applying for a Storage Provider opening](#applying-for-a-storage-provider-opening)
    - [Setup and configure the storage node](#setup-and-configure-the-storage-node)
    - [Run storage node as a service](#run-storage-node-as-a-service)
    - [Verify everything is working](#verify-everything-is-working)
- [Troubleshooting](#troubleshooting)
  - [Port not set](#port-not-set)
  - [No tokens in role account](#no-tokens-in-role-account)
  - [Install yarn and node on linux](#install-yarn-and-node-on-linux)
  - [Caddy v1 (deprecated)](#caddy-v1-deprecated)
    - [Run caddy as a service](#run-caddy-as-a-service-1)
<!-- TOC END -->



# Overview

This page contains all information required to set up your storage node and become a `Storage Provider` on the current Joystream testnet.

The guide for the `Storage Provider Lead` can be found [here](/roles/storage-lead).

# Instructions

The instructions below will assume you are running as `root`. This makes the instructions somewhat easier, but less safe and robust.

Note that this has been tested on a fresh images of `Ubuntu 20.04 LTS` and `Debian 10`.

The system has shown to be quite resource intensive, so you should choose a VPS with specs equivalent to [Linode 8GB](https://www.linode.com/pricing/) or better (not an affiliate link).

Please note that unless there are any openings for new storage providers (which you can check in [Pioneer](https://testnet.joystream.org/) under `Working Groups` -> `Opportunities`), you will not be able to join. Applying to the opening is easiest in Pioneer, but once hired, you no longer need it. Actions you may want to perform after getting hired are easiest to carry out with the [CLI](/tools/cli/README.md#working-groups). With this, you can configure things like:
- changing your reward destination address
- changing your role key
- increasing your stake
- leaving the role

## Initial setup
First, you need to connect to a fully synced [Joystream full node](https://github.com/Joystream/joystream/releases). By default, the program assumes you are running a node on the same device. For instructions on how to set this up, go [here](/roles/validators). Note that you can disregard all the parts about keys before applying, and just install the software, so it is ready to go.
We strongly encourage that you run both the [node](/roles/validators#run-as-a-service) and the other software below as a service.

First, you need to set up `node`, `npm` and `yarn`. This is sometime troublesome to do with the `apt` package manager. Go [here](#install-yarn-and-node-on-linux) to do this if you are not confident in your abilities to navigate the rough seas.

Now, get the additional dependencies:
```
$ apt-get update && apt-get upgrade -y
$ apt-get install git build-essential libtool automake autoconf python
# on debian 10
$ apt-get install libcap2-bin
```

## Install IPFS
The storage node uses [IPFS](https://ipfs.io/) as backend.
```
$ wget https://github.com/ipfs/go-ipfs/releases/download/v0.6.0/go-ipfs_v0.6.0_linux-amd64.tar.gz
$ tar -xvzf go-ipfs_v0.6.0_linux-amd64.tar.gz
$ cd go-ipfs
$ ./ipfs init --profile server
$ ./install.sh
# start ipfs daemon:
$ ipfs daemon
```
If you see `Daemon is ready` at the end, you are good!

### Configure IPFS
Some default configurations needs to be changed, in order to get better performance:

```
# cuz xyz
ipfs config --bool Swarm.DisableBandwidthMetrics true
# Default only allows storing 10GB, so:
ipfs config Datastore.StorageMax "50GB"
# cuz xyz
ipfs config --json Gateway.PublicGateways '{"localhost": null }'
```


### Run IPFS as a service

To ensure high uptime, it's best to set the system up as a `service`.

Example file below:

```
$ nano /etc/systemd/system/ipfs.service
# Paste in everything below the stapled line
---
[Unit]
Description=ipfs
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root
LimitNOFILE=8192
PIDFile=/var/run/ipfs/ipfs.pid
ExecStart=/usr/local/bin/ipfs daemon --routing=dhtclient
Restart=on-failure
RestartSec=3
StartLimitInterval=600

[Install]
WantedBy=multi-user.target
```
Save and exit. Close the `ipfs daemon` if it's still running, then:
```
$ systemctl start ipfs
# If everything works, you should get an output. Verify with:
$ systemctl status ipfs
# If you see something else than "Daemon is ready" at the end, try again in a couple of seconds.
# To have ipfs start automatically at reboot:
$ systemctl enable ipfs
# If you want to stop ipfs, either to edit the file or some other reason:
$ systemctl stop ipfs
```


## Setup Hosting
In order to allow for users to upload and download, you have to set up hosting, with an actual domain as both Chrome and Firefox requires `https://`. If you have a "spare" domain or subdomain you don't mind using for this purpose, go to your domain registrar and point your domain to the IP you want. If you don't, you will need to purchase one.

To configure SSL-certificates the easiest is to use [caddy](https://caddyserver.com/), but feel free to take a different approach. Note that if you are using caddy for commercial use, you need to acquire a license. Please check their terms and make sure you comply with what is considered personal use.

Previously, this guide was using Caddy v1, but this has now been deprecated. As some of you may already have installed it, and may want to continue running it, the now deprecated instructions can be found in full [here](#caddy-v1).

### Instructions
For the best setup, you should use the "official" [documentation](https://caddyserver.com/docs/).

The instructions below are for Caddy v2.1:
```
$ wget https://github.com/caddyserver/caddy/releases/download/v2.1.1/caddy_2.1.1_linux_amd64.tar.gz
$ tar -vxf caddy_2.1.1_linux_amd64.tar.gz
$ mv caddy /usr/bin/
# Test that it's working:
$ caddy version
```

Configure the `Caddyfile`:
```
$ nano ~/Caddyfile
# Paste in everything below the stapled line
---
# Storage Node API
<your.cool.url> {
    route /storage/* {
    reverse_proxy localhost:3000
    header /storage {
        Access-Control-Allow-Methods "GET, PUT, HEAD, OPTIONS"
    }
}
```

Now you can check if you configured correctly, with:
```
$ caddy validate ~/Caddyfile
# Which should return:
--
...
Valid configuration
--
# You can now run caddy with:
$ caddy run --config /root/Caddyfile
# Which should return something like:
--
...
... [INFO] [<your.cool.url>] The server validated our request
... [INFO] [<your.cool.url>] acme: Validations succeeded; requesting certificates
... [INFO] [<your.cool.url>] Server responded with a certificate.
... [INFO][<your.cool.url>] Certificate obtained successfully
... [INFO][<your.cool.url>] Obtain: Releasing lock
```

### Run caddy as a service
To ensure high uptime, it's best to set the system up as a `service`.

Example file below:

```
$ nano /etc/systemd/system/caddy.service
# Paste in everything below the stapled line
---
[Unit]
Description=Caddy
Documentation=https://caddyserver.com/docs/
After=network.target

[Service]
User=root
ExecStart=/usr/bin/caddy run --config /root/Caddyfile
ExecReload=/usr/bin/caddy reload --config /root/Caddyfile
TimeoutStopSec=5s
LimitNOFILE=1048576
LimitNPROC=512
PrivateTmp=true
ProtectSystem=full
AmbientCapabilities=CAP_NET_BIND_SERVICE

[Install]
WantedBy=multi-user.target
```
Save and exit. Close `caddy` if it's still running, then:
```
$ systemctl start caddy
# If everything works, you should get an output. Verify with:
$ systemctl status caddy
# Which should produce something similar to the previous output.
# To have caddy start automatically at reboot:
$ systemctl enable caddy
# If you want to stop caddy:
$ systemctl stop caddy
# If you want to edit your Caddfile, edit it, then run:
$ caddy reload
```

## Install and Set up the Storage Node

First, you need to clone the Joystream monorepo, which contains the storage software.
Note that if you already have a storage-node installed (or running), go [here](#update-your-storage-node).

```
$ git clone https://github.com/Joystream/joystream.git
$ cd joystream
$ yarn install
$ yarn run colossus --help
```
You can set the PATH to avoid the `yarn run` prefix by:
```
$ cd ~/joystream/storage-node/packages/colossus
$ yarn link
# Test that it's working with:
$ colossus --help
# It should now work globally
```

## Update Your Storage Node
To update your storage-node from an old network, do the following steps:

```
# If you are running as service (which you should)
$ systemctl stop storage-node
$ cd joystream
$ git pull origin master
$ yarn install
$ yarn run colossus --help
```

If you have been running a storage node previously, and used `.bash_profile` to avoid the `yarn run` prefix, you need to:
`$ nano ~/.bash_profile`
Then, uncomment or remove the lines below:
```
# Colossus
alias colossus="/root/storage-node-joystream/packages/colossus/bin/cli.js"  
alias helios="/root/storage-node-joystream/packages/helios/bin/cli.js"
```
For helios, you can instead change the path from `/root/storage-node-joystream/packages/helios/bin/cli.js` -> `/root/joystream/storage-node/packages/helios/bin/cli.js`
Then:

```
$ . ~/.bash_profile
$ cd ~/joystream/storage-node/packages/colossus
$ yarn link
# Test that it's working with:
$ colossus --help
```
It should now work globally.

Note that you also need to reconfigure [IPFS](#configure-ipfs).
For most users, it might be easiest to:
```
rm -rf ~/.ipfs
```
Go back to [re-install](#install-ipfs).

### Applying for a Storage Provider opening

Click [here](https://testnet.joystream.org) to open the `Pioneer app` in your browser. Then follow instructions [here](https://github.com/Joystream/helpdesk#get-started) to generate a set of `Keys`, get tokens, and sign up for a `Membership`. This `key` will be referred to as the `member` key.

Make sure to save the `5YourJoyMemberAddress.json` file. This key will require tokens to be used as stake for the `Storage Provider` application (`application stake`) and further stake may be required if you are selected for the role (`role stake`).

To check for current openings, visit [this page](https://testnet.joystream.org/#/working-groups/opportunities) on Pioneer and look for any `Storage Provider` applications which are open for applications. If there is an opening available, fill in the details requested in the form required and stake the tokens needed to apply (when prompted you can sign a transaction for this purpose).

During this process you will be provided with a role key, which will be made available to download in the format `5YourStorageAddress.json`. If you set a password for this key, remember it :)

The next steps (below) will only apply if you are a successful applicant.


### Setup and configure the storage node

**Make sure your [Joystream full node](https://github.com/Joystream/joystream/releases) is fully synced before you move to the next step(s)!**

Assuming you are running the storage node on a VPS via ssh, on your local machine:

```
# Go the directory where you saved your <5YourStorageAddress.json>:
$ scp <5YourStorageAddress.json> <user>@<your.vps.ip.address>:/path/to/joystream/storage-node/
```
Your `5YourStorageAddress.json` should now be where you want it.

On the machine/VPS you want to run your storage node:

```
# If you are not already in that directory:
$ cd /path/to/joystream/storage-node
```

On our older testnets, at this point you would have to "apply" using a separate colossus command to any available storage role. With the evolution of our testnet and the introduction of the `Storage Working Group`, this is no longer necessary. The next steps simply require that you link the "role key" (`5YourStorageAddress.json`) and `Storage ID` to your storage server.

To check your `Storage ID`, you have two (easy) options:
1. Use the [CLI](/tools/cli/README.md#working-groups:overview)
2. Check [Pioneer](https://testnet.joystream.org/#/working-groups)

**Note:** Make sure you send some tokens to your "role key"/`5YourStorageAddress.json` before proceeding! It needs tokens to send transactions, or it will be considered "down", and unavailable for syncing.

```
# To make sure everything is running smoothly, it would be helpful to run with DEBUG.
# If you used "yarn link":
$ DEBUG=* colossus server --key-file <5YourStorageAddress.json> --public-url https://<your.cool.url>/storage/ --provider-id <your_storage-id>

# If not:
$ cd ~/joystream
$ DEBUG=* yarn run colossus server --key-file <5YourStorageAddress.json> --public-url https://<your.cool.url>/storage/ --provider-id <your_storage-id>

# If you set a passphrase for <5YourStorageAddress.json>:
$ DEBUG=* (yarn run) colossus server --key-file <5YourStorageAddress.json> --public-url https://<your.cool.url>/storage/ --provider-id <your_storage-id> --passphrase <your_passphrase>
```

If you do this, you should see (among other things) something like:

```
<timestamp> localhost node[36281]: <timestamp> joystream:discovery:publish {
<timestamp> localhost node[36281]:   name: 'Qm...fF',
<timestamp> localhost node[36281]:   value: '/ipfs/Qm...12'
<timestamp> localhost node[36281]: }
<timestamp> localhost node[36281]: <timestamp> joystream:runtime:base:tx Submitted: {"nonce":<n>,"txhash":"0xf7d...46fd","tx":"0x...46"}
<timestamp> localhost node[36281]: <timestamp> joystream:runtime:base:tx Finalized {"nonce":<n>,"txhash":"0xf7d...46fd"}
<timestamp> localhost node[36281]: <timestamp> joystream:colossus publishing complete, scheduling next update

```

If everything is working smoothly, you will now start syncing the `content directory`.

Note that unless you run this is a [service](#run-storage-node-as-a-service), you now have to open a second terminal for the remaining steps.

#### Check that you are syncing
In your second terminal window:
```
$ ipfs bitswap wantlist
---
# Output should be a long list of keys, eg. Note that it might take a few minutes before the actual content from the Joystream content directory shows up.
---
QmeszeBjBErFQrkiQPh8QhTs3hfCEGJuK2jNopatHnps1k
...
QmfCbUsYhKBmrdop3yFrerqVKwBJvY5tbpV1cf9Cx3L1J8
```
If you did this immediately after FIRST starting your storage node, the `wantlist` might be empty. Give it a minute, and it should contain at least the number of items in the content directory. You can also check what content you have stored by:
```
$ ipfs refs local
---
# Output should be an even longer list of keys, eg.
---
QmeszeBjBErFQrkiQPh8QhTs3hfCEGJuK2jNopatHnps1k
Qmezum3AWdxkm1AtHe35DZGWdfhTQ4PVmmZatGwDL68RES
...
QmfCCjC5w9wxTFoAaJ947ss2oc1jx6R2mM9xjU7Ccrq55M
QmfCbUsYhKBmrdop3yFrerqVKwBJvY5tbpV1cf9Cx3L1J8
```
Another thing you can monitor:
```
$ ipfs stats repo
---
# Should return the size and objects, eg:
---
NumObjects: 98416
RepoSize:   25544041095
StorageMax: 50000000000
RepoPath:   /root/.ipfs
Version:    fs-repo@10
```
`RepoSize` will grow rapidly during sync.

### Run storage node as a service

To ensure high uptime, it's best to set the system up as a `service`. Note that this will not work if you set a password for your `<5YourStorageAddress.json> `.

Example file below:

```
$ nano /etc/systemd/system/storage-node.service
# Paste in everything below the stapled line
---
[Unit]
Description=Joystream Storage Node
After=network.target ipfs.service joystream-node.service

[Service]
User=root
WorkingDirectory=/root/joystream/storage-node
LimitNOFILE=8192
Environment=DEBUG=joystream:*,-joystream:util:ranges
ExecStart=/usr/local/lib/nodejs/node-v12.18.2-linux-x64/bin/node packages/colossus/bin/cli.js \
        --key-file <5YourStorageAddress.json> \
        --public-url https://<your.cool.url>/storage/ \
        --provider-id <your_storage-id>
Restart=on-failure
StartLimitInterval=600

[Install]
WantedBy=multi-user.target
```
Save and exit. Close the running `colossus` if it's still running, then:
```
$ systemctl start storage-node
# If everything works, you should get an output. Verify with:
$ systemctl status storage-node
# Which should produce something like:
---
● storage-node.service - Joystream Storage Node
...

<timestamp> localhost node[36281]: <timestamp> joystream:sync Starting sync run...
<timestamp> localhost node[36281]: <timestamp> joystream:sync sync run complete
<timestamp> localhost node[36281]: <timestamp> joystream:sync Starting sync run...
<timestamp> localhost node[36281]: <timestamp> joystream:sync sync run complete
...
---
# To have colossus start automatically at reboot:
$ systemctl enable storage-node
# If you want to stop the storage node, either to edit the storage-node.service file or some other reason:
$ systemctl stop storage-node
```

### Verify everything is working

In your browser, find and click on an uploaded media file [here](https://testnet.joystream.org//#/media/), then open the developer console, and find the URL of the asset. Copy the `<content-id>`, i.e. whatever comes after the last `/`.

Then paste the following in your browser:
`https://<your.cool.url>/storage/swagger.json`
Which should return a json.

And:
`https://<your.cool.url>/storage/asset/v0/<content-id>`.
(e.g. `5GPhGYaGumtdpFYowMHY15hsdZVZUyEUe2trgh2vq7zGcFKx`)
If the content starts playing, that means you are good!

# Troubleshooting
If you had any issues setting it up, you may find your answer here!

## Port not set

If you get an error like this:
```
Error: listen EADDRINUSE: address already in use :::3000
```

It most likely means your port is blocked. This could mean your storage-node is already running (in which case you may want to kill it unless it's configured as a service), or that another program is using the port.

In case of the latter, you can specify a new port (e.g. 3001) with the `--port 3001` flag.
Note that you have to modify the `Caddyfile` as well...

## No tokens in role account
If you try to run the storage-node without tokens to pay the transaction fee, you may at some point have tried so many times your transaction gets "temporarily banned". In this case, you either have to wait for a while, or use the [CLI](/tools/cli/README.md#working-groups:updateRoleAccount) tool to change your "role account".

## Install yarn and node on linux

Go [here](https://nodejs.org/en/download/) and find the newest (LTS) binary for your distro. This guide will assume 64-bit linux, and `node-v12.18.2`.

If you want to install as `root`, so your user can use `npm` without `sudo` privileges, go [here](#install-as-root).

If you want to install as another user (must have `sudo` privileges), go [here](#install-as-user-with-sudo-privileges).

Alternatives such as [nvm](https://github.com/nvm-sh/nvm) or [nodesource](https://github.com/nodesource/distributions/blob/master/README.md) are also worth considering.

#### Install as Root
This section assumes you are installing as `root`. It also demonstrates how you can provide another user access without having to use `sudo`. It doesn't matter if user `joystream` has `sudo` privileges or not.

```
$ wget https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz
$ mkdir -p /usr/local/lib/nodejs
$ tar -xJvf node-v12.18.2-linux-x64.tar.xz -C /usr/local/lib/nodejs
$ nano ~/.bash_profile
---
Append the following lines:
---
# Nodejs
VERSION=v12.18.2
DISTRO=linux-x64
export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH
```
Save and exit, then:
```
$ source ~/.bash_profile
# Verify version:
$ node -v
$ npm -v
$ npx -v
# Install yarn
$ npm install yarn -g
# If everything looks ok, and you want to allow user joystream access:
$ chown -R joystream /usr/local/lib/nodejs
```
Log in to joystream:
```
$ su joystream
$ cd
# Repeat the .bash_profile config:
$ nano ~/.bash_profile
---
Append the following lines:
---
# Nodejs
VERSION=v12.18.2
DISTRO=linux-x64
export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH
```
Save and exit, then:
```
$ source ~/.bash_profile
# Verify that it works:
$ node -v
$ npm -v
$ npx -v
$ yarn -v
```

You have now successfully installed the newest (LTS) versions of `npm`, `node` and `yarn`.

#### Install as user with `sudo` privileges
This section assumes the steps are performed as user `joystream` with `sudo` privileges.

As `joystream`
```
$ wget https://nodejs.org/dist/v12.18.2/node-v12.18.2-linux-x64.tar.xz
$ mkdir -p /usr/local/lib/nodejs
$ tar -xJvf node-v12.18.2-linux-x64.tar.xz -C /usr/local/lib/nodejs
$ nano ~/.bash_profile
---
Append the following lines:
---
# Nodejs
VERSION=v12.18.2
DISTRO=linux-x64
export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH
```
Save and exit, then:
```
$ source ~/.bash_profile
$ sudo chown -R joystream /usr/local/lib/nodejs
# Verify that it works:
$ node -v
$ npm -v
$ npx -v
# Install yarn
$ npm install yarn -g
# Verify that it works:
$ yarn -v
```
If you want `root` to be able to use `npm` as well:

```
$ sudo su
$ nano ~/.bash_profile
---
Append the following lines:
---
# Nodejs
VERSION=v12.18.2
DISTRO=linux-x64
export PATH=/usr/local/lib/nodejs/node-$VERSION-$DISTRO/bin:$PATH
```
Save and exit, then:

`$ source ~/.bash_profile`

You have now successfully installed the newest (LTS) versions of `npm`, `node` and `yarn`.


## Caddy v1 (deprecated)

These instructions below are for Caddy v1. If you don't already have it installed, it will not work. The instructions are only kept in case you happen to have installed it on your computer/VPS already.

```
$ curl https://getcaddy.com | bash -s personal
# Allow caddy access to required ports:
$ setcap 'cap_net_bind_service=+ep' /usr/local/bin/caddy
$ ulimit -n 8192
```

Configure a caddy with `nano ~/Caddyfile` and paste in the following:

```
# Storage Node API
https://<your.cool.url> {
    proxy / localhost:3000 {
        transparent
    }
    header / {
        Access-Control-Allow-Origin  *
        Access-Control-Allow-Methods "GET, PUT, HEAD, OPTIONS"
    }
}
```
Now you can check if you configured correctly, with:
```
$ /usr/local/bin/caddy --validate --conf ~/Caddyfile
# Which should return:
Caddyfile is valid

# You can now run caddy with:
$ (screen) /usr/local/bin/caddy --agree --email <your_mail@some.domain> --conf ~/Caddyfile
```
After a short wait, you should see:
```
YYYY/MM/DD HH:NN:SS [INFO] [<your.cool.url>] Server responded with a certificate.
done.

Serving HTTPS on port 443
https://<your.cool.url>


Serving HTTP on port 80
https://<your.cool.url>

```

### Run caddy as a service
To ensure high uptime, it's best to set the system up as a `service`.

Example file below:

```
$ nano /etc/systemd/system/caddy.service
# Paste in everything below the stapled line
---
[Unit]
Description=Reverse proxy for storage node
After=network.target

[Service]
User=root
WorkingDirectory=/root
LimitNOFILE=8192
PIDFile=/var/run/caddy/caddy.pid
ExecStart=/usr/local/bin/caddy -agree -email <your_mail@some.domain> -pidfile /var/run/caddy/caddy.pid -conf /root/Caddyfile
Restart=on-failure
StartLimitInterval=600


[Install]
WantedBy=multi-user.target
```
Save and exit. Close `caddy` if it's still running, then:
```
$ systemctl start caddy
# If everything works, you should get an output. Verify with:
$ systemctl status caddy
# Which should produce something like:
---
● caddy.service - Reverse proxy for storage node
   Loaded: loaded (/etc/systemd/system/caddy.service; disabled)
   Active: active (running) since Day YYYY/MM/DD HH:NN:SS UTC; 6s ago
 Main PID: 9053 (caddy)
   CGroup: /system.slice/caddy.service
           9053 /usr/local/bin/caddy -agree email <your_mail@some.domain> -pidfile /var/run/caddy/caddy.pid -conf /root/Caddyfile

Mon DD HH:NN:SS localhost systemd[1]: Started Reverse proxy for hosted apps.
Mon DD HH:NN:SS localhost caddy[9053]: Activating privacy features... done.
Mon DD HH:NN:SS localhost caddy[9053]: Serving HTTPS on port 443
Mon DD HH:NN:SS localhost caddy[9053]: https://<your.cool.url>
Mon DD HH:NN:SS localhost caddy[9053]: https://<your.cool.url>
Mon DD HH:NN:SS localhost caddy[9053]: Serving HTTP on port 80
Mon DD HH:NN:SS localhost caddy[9053]: https://<your.cool.url>
---
# To have caddy start automatically at reboot:
$ systemctl enable caddy
# If you want to stop caddy, either to edit the file or some other reason:
$ systemctl stop caddy
```
