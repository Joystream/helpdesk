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
  - [Caddy v1 (deprecated)](#caddy-v1-deprecated)
    - [Run caddy as a service](#run-caddy-as-a-service-1)
<!-- TOC END -->



# Overview

This page contains all information required to set up your storage node and become a `Storage Provider` on the current Joystream testnet.

The guide for the `Storage Provider Lead` can be found [here](/roles/storage-lead).

# Instructions

The instructions below will assume you are running as `root`. This makes the instructions somewhat easier, but less safe and robust.

Note that this has been tested on a fresh images of `Ubuntu 20.04 LTS`. You may run into some troubles with `Debian`.

The system has shown to be quite resource intensive, so you should choose a VPS with specs equivalent to [Linode 8GB](https://www.linode.com/pricing/) or better (not an affiliate link).

Please note that unless there are any openings for new storage providers (which you can check in [Pioneer](https://testnet.joystream.org/) under `Working Groups` -> `Opportunities`), you will not be able to join. Applying to the opening is easiest in Pioneer, but once hired, you no longer need it. Actions you may want to perform after getting hired are easiest to carry out with the [CLI](/tools/cli/README.md#working-groups). With this, you can configure things like:
- changing your reward destination address
- changing your role key
- increasing your stake
- leaving the role

## Initial setup
First of all, you need to connect to a fully synced [Joystream full node](https://github.com/Joystream/joystream/releases). By default, the program assumes you are running a node on the same device. For instructions on how to set this up, go [here](/roles/validators). Note that you can disregard all the parts about keys before applying, and just install the software so it is ready to go.
We strongly encourage that you run both the [node](/roles/validators#run-as-a-service) and the other software below as a service.

Now, get the additional dependencies:
```
$ apt-get update && apt-get upgrade -y
# on debian 10, if you manage the first hurdle:
$ apt-get install libcap2-bin
```

## Install IPFS
The storage node uses [IPFS](https://ipfs.io/) as backend.
```
$ wget https://github.com/ipfs/go-ipfs/releases/download/v0.8.0/go-ipfs_v0.8.0_linux-amd64.tar.gz
$ tar -xvzf go-ipfs_v0.8.0_linux-amd64.tar.gz
$ cd go-ipfs
$ ./ipfs init --profile server
$ ./install.sh
# start ipfs daemon:
$ ipfs daemon
```
If you see `Daemon is ready` at the end, you are good!

### Configure IPFS
Some of the default configurations needs to be changed, in order to get better performance:

```
# cuz xyz
ipfs config --bool Swarm.DisableBandwidthMetrics true
# Default only allows storing 10GB, so:
ipfs config Datastore.StorageMax "400GB"
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
LimitNOFILE=10240
PIDFile=/run/ipfs/ipfs.pid
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
In order to allow for users to upload and download, you have to setup hosting, with an actual domain as both Chrome and Firefox requires `https://`. If you have a "spare" domain or subdomain you don't mind using for this purpose, go to your domain registrar and point your domain to the IP you want. If you don't, you will need to purchase one.

To configure SSL-certificates the easiest is to use [caddy](https://caddyserver.com/), but feel free to take a different approach. Note that if you are using caddy for commercial use, you need to acquire a license. Please check their terms and make sure you comply with what is considered personal use.

Previously, this guide was using Caddy v1, but this has now been deprecated. As some of you may already have installed it, and may want to continue running it, the now deprecated instructions can be found in full [here](#caddy-v1).

### Instructions
For the best setup, you should use the "official" [documentation](https://caddyserver.com/docs/).

The instructions below are for Caddy v2.4.1:
```
$ wget https://github.com/caddyserver/caddy/releases/download/v2.4.1/caddy_2.4.1_linux_amd64.tar.gz
$ tar -vxf caddy_2.4.1_linux_amd64.tar.gz
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
https://<your.cool.url>/storage/* {
        route /storage/* {
                uri strip_prefix /storage
                reverse_proxy localhost:3000
        }
        header /storage {
                Access-Control-Allow-Methods "GET, PUT, HEAD, OPTIONS"
        }
        request_body {
                max_size 10GB
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

## Install and Setup the Storage Node

First, you need to clone the Joystream monorepo, which contains the storage software.
Note that if you already have a storage-node installed (or running), go [here](#update-your-storage-node).

```
$ git clone https://github.com/Joystream/joystream.git
$ cd joystream
$ ./setup.sh
# this requires you to start a new session. if you are using a vps:
$ exit
$ ssh user@ipOrURL
# on your local machine, just close the terminal and open a new one
$ yarn build:packages
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
To update your storage-node from an old network, it's probably time to update `ipfs` and `caddy`, although older versions _should_ continue to work.

If you `rm -rf ~/.ipfs`, you are also saving a **lot** of storage space, as the content-directory will not be migrated in full.

There are also some changes required in all the .service files, so ideally go through the entire guide!

To upgrade the storage node itself:
```
# If you are running as service (which you should)
$ systemctl stop storage-node
$ cd ~/joystream/storage-node/packages/colossus
$ yarn unlink
$ cd ~/joystream
$ git pull origin master
$ rm -rf node modules
$ yarn cache clean
$ ./setup.sh
# this requires you to start a new session. if you are using a vps:
$ exit
$ ssh user@ipOrURL
# on your local machine, just close the terminal and open a new one
$ cd ~/joystream
$ yarn build:packages
$ cd ~/joystream/storage-node/packages/colossus
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
$ scp <5YourStorageAddress.json> <user>@<your.vps.ip.address>:/root/joystream/storage-node/
```
Your `5YourStorageAddress.json` should now be where you want it.

On the machine/VPS you want to run your storage node:

```
# If you are not already in that directory:
$ cd ~/joystream/storage-node
```

On our older testnets, at this point you would have to "apply" using a separate colossus command to any available storage role. With the evolution of our testnet and the introduction of the `Storage Working Group`, this is no longer necessary. The next steps simply require that you link the "role key" (`5YourStorageAddress.json`) and `Storage ID` to your storage server.

To check your `Storage ID`, you have two (easy) options:
1. Use the [CLI](/tools/cli/README.md#working-groups:overview)
2. Check [Pioneer](https://testnet.joystream.org/#/working-groups)

**Note:** Make sure you send some tokens to your "role key"/`5YourStorageAddress.json` before proceeding! It needs tokens to send transactions, or it will be considered "down", and unavailable for syncing.

```
# To make sure everything is running smoothly, it would be helpful to run with DEBUG.

$ cd ~/joystream
$ DEBUG=joystream:* yarn run colossus server --key-file <5YourStorageAddress.json> --public-url https://<your.cool.url>/storage/ --provider-id <your_storage-id>

# If you set a passphrase for <5YourStorageAddress.json>:
$ DEBUG=joystream:* (yarn run) colossus server --key-file <5YourStorageAddress.json> --public-url https://<your.cool.url>/storage/ --provider-id <your_storage-id> --passphrase <your_passphrase>
```

If you do this, you should see (among other things) something like:

```
... :  ________                     _____
... :  ______(_)__________  __________  /__________________ _______ ___
... :  _____  /_  __ \_  / / /_  ___/  __/_  ___/  _ \  __ `/_  __ `__ \
... :  ____  / / /_/ /  /_/ /_(__  )/ /_ _  /   /  __/ /_/ /_  / / / / /
... :  ___  /  \____/_\__, / /____/ \__/ /_/    \___/\__,_/ /_/ /_/ /_/
... :  /___/         /____/
... :  <timestamp>joystream:runtime:base Init
... :  <timestamp>joystream:runtime:identities Init
... :  <timestamp>joystream:runtime:identities Initializing key from /root/ <5YourStorageAddress.json>
... :  <timestamp>joystream:runtime:identities Successfully initialized with address  <5YourStorageAddress>
... :  <timestamp>joystream:runtime:balances Init
... :  <timestamp>joystream:runtime:roles Init
... :  <timestamp>joystream:runtime:assets Init
... :  <timestamp>joystream:runtime:system Init
... :  <timestamp>joystream:runtime:base Waiting for chain to be synced before proceeding.
... :  <timestamp>joystream:sync Sync run started.
... :  [HPM] Proxy created: function (path, req) {
... :    // we get the full path here so it needs to match the path where
... :    // it is used by the openapi initializer
... :    return path.match('^/asset/v0') && (req.method === 'GET' || req.method === 'HEAD')
... :  }  -> http://localhost:8080/
... :  Starting API server...
... :  API server started. { address: '::', family: 'IPv6', port: 3000 }
... :  <timestamp>joystream:storage:storage IPFS node is up with identity:  <ipfsPeerId>
... :  <timestamp>joystream:colossus announcing public url
... :  <timestamp>joystream:sync Sync run completed, set <n> new relationships to ready
... :  <timestamp>joystream:runtime:base:tx Submitted: {"nonce":"<nonce>","txhash":"<hash>","tx":"<hash>"}
... :  <timestamp>joystream:runtime:base:tx Finalized {"nonce":"<nonce>","txhash":"<hash>"}
```

If everything is working smoothly, you will now start syncing the `content directory`.

Note that unless you run this is a [service](#run-storage-node-as-a-service), you now have to open a second terminal for the remaining steps.

#### Check that you are syncing
After you've had it running for a bit (>1 min):
```
$ cd ~/joystream/
$ yarn run helios
```
If everything is working, you should rather quickly, see your SP as active, with correct `workerId` and URL.

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
ExecStart=/root/.volta/bin/node \
        packages/colossus/bin/cli.js \
        --key-file <5YourStorageAddress.json> \
        --public-url https://<your.cool.url>/storage/ \
        --provider-id <your_storage-id>
Restart=on-failure
StartLimitInterval=600

[Install]
WantedBy=multi-user.target
```
Save and exit. Close `colossus` if it's still running, then:
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

In your browser, find and click on an uploaded media file [here](https://testnet.joystream.org//#/media/), then open the developer console, and find the URL of the asset. Copy the `<content-id>`, ie. whatever comes after the last `/`.

Then paste the following in your browser:
`https://<your.cool.url>/storage/swagger.json`
Which should return a json.

And:
`https://<your.cool.url>/storage/asset/v0/<content-id>`.
(eg. `5GPhGYaGumtdpFYowMHY15hsdZVZUyEUe2trgh2vq7zGcFKx`)
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


## Caddy v1 (deprecated)

These instructions below are for Caddy v1. If you don't already have it installed, it will not work. The instructions are only kept in case you happen to have installed it on your computer/VPS already.

```
$ curl https://getcaddy.com | bash -s personal
# Allow caddy access to required ports:
$ setcap 'cap_net_bind_service=+ep' /usr/local/bin/caddy
$ ulimit -n 8192
```

Configure caddy with `nano ~/Caddyfile` and paste in the following:

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
