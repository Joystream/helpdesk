<p align="center"><img src="img/validator_new.svg"></p>

<div align="center">
  <h4>This is a step-by-step guide to setup your <a href="https://github.com/Joystream/substrate-node-joystream">full node</a>, and get started as a Validator on the latest
  <a href="https://testnet.joystream.org">Joystream Testnet</a>.<h4>
</div>



Table of Contents
==

<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
- [Overview](#overview)
- [Instructions](#instructions)
- [On Your Machine](#on-your-machine)
  - [Mac](#mac)
      - [Setup Node](#setup-node)
      - [Keys](#keys)
      - [Final Step](#final-step)
  - [Linux](#linux)
      - [Setup Node](#setup-node-1)
      - [Keys](#keys-1)
      - [Final Step](#final-step-1)
- [In the Pioneer app (browser)](#in-the-pioneer-app-browser)
  - [Validator Setup](#validator-setup)
      - [Generate your keys](#generate-your-keys)
      - [Configure your validator keys](#configure-your-validator-keys)
- [Advanced](#advanced)
  - [Run as a service](#run-as-a-service)
      - [Configure the service](#configure-the-service)
      - [Starting the service](#starting-the-service)
      - [Errors](#errors)
  - [Settings](#settings)
      - [Bonding preferences](#bonding-preferences)
      - [Validating preferences](#validating-preferences)
  - [Nominating](#nominating)
      - [Generate your keys](#generate-your-keys-1)
      - [Configure your validator keys](#configure-your-validator-keys-1)
- [Troubleshooting](#troubleshooting)
<!-- TOC END -->

# Overview

This page contains all information on how to setup your node and becoming a `Validator` on the Joystream Testnets. It will be updated for improvements, and when something changes for new testnets.

If you want to earn more `Joy` tokens, but for some reason can't or won't become a `Validator`, you can [`Nominate`](#nominating) instead.

# Instructions

The instructions below covers Mac and Linux (x86_64 and armv7). Windows binaries are currently not available. As a general note, remember to use your `stash` key when setting the `memo` to qualify for the monero rewards, not controller this time!

**Note**
If you are just running a node, and don't want to be a `Validator`, you can skip the flags
`--pruning archive` and `--validator`


# On Your Machine

---

## Mac

* Every time something is written in `<brackets>`, it means you have to replace this with your input, without the `<>`.
* When something is written in `"double_quotes"`, it means the number/data will vary depending on your node or the current state of the blockchain.
* For terminal commands, `$` means you must type what comes after that on windows and mac respectively. `#` Means it's just a comment/explanation, and must not be typed.
```
# This is just a comment, don't type or paste it in your terminal!
$ cd ~/
# Only type/paste the "cd ~/, not the preceding $ !
```
#### Setup Node

Open the terminal (Applications->Utilities):

```
$ cd ~/
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v2.1.2/joystream-node-2.1.2-441c04b-x86_64-macos.tar.gz
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v2.1.2/rome-testnet.json
----
# If you don't have wget installed, paste the link in your browser save.
# Assuming it gets saved in your ~/Downloads folder:
$ mv ~/Downloads/joystream-node-2.1.2-441c04b-x86_64-macos.tar.gz ~/
---
$ tar -vxf joystream-node-2.1.2-441c04b-x86_64-macos.tar.gz
$ ./joystream-node --chain rome-testnet.json --pruning archive --validator
```
- If you want your node to have a non-random identifier, add the flag `--name <nodename>`
- If you want to get a more verbose log output, add the flag `<nodename> --log runtime`

Your node should now start syncing the blockchain. The output should look like this:
```
Joystream Node
  version "Version"-"your_OS"
  by Joystream, 2019
Chain specification: "Joystream Version"
Node name: "nodename"
Roles: AUTHORITY
Initializing Genesis block/state (state: "0x…", header-hash: "0x…")
Loading GRANDPA authority set from genesis on what appears to be first startup.
Loaded block-time = BabeConfiguration { slot_duration: 6000, epoch_length: 100, c: (1, 4), genesis_authorities: ...
Creating empty BABE epoch changes on what appears to be first startup.
Highest known block at #0
Local node identity is: "peer id"
Starting BABE Authorship worker
Discovered new external address for our node: /ip4/"IP"/tcp/30333/p2p/"peer id"
New epoch 0 launching at block ...
...
...
Syncing, target=#"block_height" ("n" peers), best: #"synced_height" ("hash_of_synced_tip"), finalized #0 ("hash_of_finalized_tip"), ⬇ "download_speed"kiB/s ⬆ "upload_speed"kiB/s
```
From the last line, notice `target=#"block_height"` and `best: #"synced_height"`
When the `target=#block_height`is the same as `best: #"synced_height"`, your node is fully synced!

**Keep the terminal window open.**

#### Keys

Now you need to generate your keys. Go [here](#generate-your-keys) to do that now.

#### Final Step

Now it's time to configure your keys to start validating. Go [here](#configure-your-validator-keys) to configure your `Validator`.

---

## Linux

* Every time something is written in `<brackets>`, this means you have to replace this with your input, without the `<>`.
* When something is written in `"double_quotes"`, it means the number/data will vary depending on your node or the current state of the blockchain.
* For terminal commands, `$` means you must type what comes after that on windows and mac respectively. `#` Means it's just a comment/explanation, and must not be typed.
```
# This is just a comment, don't type or paste it in your terminal!
$ cd ~/
# Only type/paste the "cd ~/, not the preceding $ !
```
#### Setup Node

Open the terminal:

```
$ cd ~/
# 64 bit debian based Linux
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v2.1.2/joystream-node-2.1.2-441c04b-x86_64-linux-gnu.tar.gz
$ tar -vxf joystream-node-2.1.2-441c04b-x86_64-linux-gnu.tar.gz
# armv7 (raspberry pi)
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v2.1.2/joystream-node-armv7-linux-gnueabihf.tar.gz
$ tar -joystream-node-armv7-linux-gnueabihf.tar.gz
# For both
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v2.1.2/rome-testnet.json
$ $ ./joystream-node --chain rome-testnet.json --pruning archive --validator
```
- If you want your node to have a non-random identifier, add the flag `--name <nodename>`
- If you want to get a more verbose log output, add the flag `<nodename> --log runtime`

Your node should now start syncing the blockchain. The output should look like this:
```
Joystream Node
  version "Version"-"your_OS"
  by Joystream, 2019
Chain specification: "Joystream Version"
Node name: "nodename"
Roles: AUTHORITY
Initializing Genesis block/state (state: "0x…", header-hash: "0x…")
Loading GRANDPA authority set from genesis on what appears to be first startup.
Loaded block-time = BabeConfiguration { slot_duration: 6000, epoch_length: 100, c: (1, 4), genesis_authorities: ...
Creating empty BABE epoch changes on what appears to be first startup.
Highest known block at #0
Local node identity is: "peer id"
Starting BABE Authorship worker
Discovered new external address for our node: /ip4/"IP"/tcp/30333/p2p/"peer id"
New epoch 0 launching at block ...
...
...
Syncing, target=#"block_height" ("n" peers), best: #"synced_height" ("hash_of_synced_tip"), finalized #0 ("hash_of_finalized_tip"), ⬇ "download_speed"kiB/s ⬆ "upload_speed"kiB/s
```
From the last line, notice `target=#"block_height"` and `best: #"synced_height"`
When the `target=#block_height`is the same as `best: #"synced_height"`, your node is fully synced!

**Keep the terminal window open.**

#### Keys

Now you need to generate your keys. Go [here](#generate-your-keys) to do that now.

#### Final Step

Now it's time to configure your keys to start validating. Go [here](#configure-your-validator-keys) to configure your `Validator`.

---

# In the Pioneer app (browser)

## Validator Setup

#### Generate your keys

While the node is syncing, you can start the process of setting up the rest.

1. Go to the [Pioneer App](https://testnet.joystream.org/), and select `My keys` in the sidebar. Click the `Create keys` tab.

Names are entirely optional, but the next steps will be easier if you follow the system suggested.

2. For ease of use, name your first keypair "stash", or at least something that contains the word.

If you want to be able to recover your keys later, write down your mnemonic seed, key pair crypto type and secret derivation path.

3. Depending on your browser, you might have to confirm saving the json file.

4. Repeat the process for your "controller" key.

You should now have two sets of keys, namely:
- the "stash" key that will stake your funds
- the "controller" key that you will use to operate your validator

5. If you already have tokens, transfer the bulk to your "stash" account. If you don't yet have any tokens, [click here](https://faucet.joystream.org/). Solve the captcha, and you should receive tokens.

If you want/need more, ask in the telegram chat. Note that long time followers will receive more tokens than newcomers.

6. Send some tokens to your "controller". It needs to perform at least two transactions, but better to send ~10.

#### Configure your validator keys

In order to be a `Validator`, you need to stake. Note that you may have to refresh your browser if you're not seeing the options right away.

**IMPORTANT:** Read step 6. carefully. Your node needs to be fully synced, before proceeding to step 7.
1. In a terminal window on the machine/VPS your node is running, paste the following:
```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933
```
If your node is running, this should return:
```
{"jsonrpc":"2.0","result":"0xa0very0long0hex0string","id":1}
```

This will save the session keys to your node. Make sure you don't close the window before copying the `0xa0very0long0hex0string` somewhere.

If your node is not running, is running on a different port, or `curl` is not installed, it will return something like:
```
curl: (7) Failed to connect to localhost port 9933: Connection refused
# or
{"jsonrpc":"2.0","error":{"code":-32601,"message":"Method not found"},"id":1}
```

2. Back in [Pioneer](https://testnet.joystream.org/), click `Validators` in the sidebar, and then the `Account actions` tab.
3. Click the `+ New stake` button, and select the keys from the first two dropdowns.
4. In the third field, enter the amount you want to stake (the maximum amount is the tokens in the account -1).
5. In the bottom dropdown, select the payment destination. Your selection here depends on your preferences.
6. If the transaction goes through, you should now see a `Set Session Key` button next to your "stash" and "controller" keys in this window. Click it, paste in your `0xa0very0long0hex0string` in the field, and confirm.
7. If the transaction goes through, you should now see a `Validate` button instead. Click it, and set your `reward commission`. Your selection here depends on your preferences.

Refresh your browser, and select the `Staking overview` tab. If your account shows under `next up`, wait for the next `era`, and you will be moved to the `validators` list.

# Advanced

## Run as a service

If you are running your node on a [Linux](#linux) and want to run it as a [service](https://wiki.debian.org/systemd/Services), you can set it up this way.
Note that you should avoid this unless you know what you are doing, are running your node on **your own VPS** or a single board computer. With great (sudo) privileges, comes great responsibilities!

If you are already running as a `validator`, consider [unstaking](#unstaking) first, as you may experience some downtime if you make any mistakes in the setup.

#### Configure the service

Either as root, or a user with sudo privileges. If the latter, add `sudo` before commands.

```
$ cd /etc/systemd/system
# you can choose whatever name you like, but the name has to end with .service
$ touch joystream-node.service
# open the file with your favorite editor (I use nano below)
$ nano joystream-node.service
```

##### Example with user joystream

The example below assumes the following:
- You want to restart your node every 24h (`86400`s)
- You have setup a user `joystream` to run the node
- The path to the `joystream-node` binary is `/home/joystream/joystream-node`

```
[Unit]
Description=Joystream Node
After=network.target

[Service]
Type=simple
User=joystream
WorkingDirectory=/home/joystream/
ExecStart=/home/joystream/joystream-node \
        --chain rome-testnet.json \
        --pruning archive \
        --validator \
        --name <nodename>
Restart=always
RuntimeMaxSec=86400
RestartSec=3
LimitNOFILE=8192

[Install]
WantedBy=multi-user.target
```

If you just want to have the node restart if it crashes, replace:

```
Restart=always
RuntimeMaxSec=86400
# with
Restart=on-failure
```


##### Example as root

The example below assumes the following:
- You want to restart your node every 24h (`86400`s)
- You have setup a user `root` to run the node
- The path to the `joystream-node` binary is `/root/joystream-node`

```
[Unit]
Description=Joystream Node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root/
ExecStart=/root/joystream-node \
        --chain rome-testnet.json \
        --pruning archive \
        --validator \
        --name <nodename>
Restart=always
RuntimeMaxSec=86400
RestartSec=3
LimitNOFILE=8192

[Install]
WantedBy=multi-user.target
```

If you just want to have the node restart if it crashes, replace:

```
Restart=always
RuntimeMaxSec=86400
# with
Restart=on-failure
```

#### Starting the service

You can add/remove any `flags` as long as you remember to include `\` for every line but the last. Also note that systemd is very sensitive to syntax, so make sure there are no extra spaces before or after the `\`.

After you are happy with your configuration:

```
$ systemctl daemon-reload
# this is only strictly necessary after you changed the .service file after running, but chances are you will need to use it once or twice.
# if your node is still running, now is the time to kill it.
$ systemctl start joystream-node
# if everything is correctly configured, this command will not return anything.
# To verify it's running:
$ systemctl status joystream-node
# this will only show the last few lines. To see the latest 100 entries (and follow as new are added)
$ journalctl -n 100 -f -u joystream-node

# To make the service start automatically at boot:
$ systemctl enable joystream-node
```
You can restart the service with:
- `systemctl restart joystream-node`

If you want to change something (or just stop), run:
- `systemctl stop joystream-node`

Before you make the changes. After changing:

```
$ systemctl daemon-reload
$ systemctl start joystream-node
```

#### Errors

If you make a mistake somewhere, `systemctl start joystream-node` will prompt:
```
Failed to start joystream-node.service: Unit joystream-node.service is not loaded properly: Invalid argument.
See system logs and 'systemctl status joystream-node.service' for details.
```
Follow the instructions, and see if anything looks wrong. Correct it, then:

```
$ systemctl daemon-reload
$ systemctl start joystream-node
```

## Settings

If you don't want to use the default settings, here are some of the options you can configure.

#### Bonding preferences
The bonding preferences decide on how your (Joy) staking rewards are distributed. There are three alternatives:
1. `Stash account (increase the amount at stake)` (default).

This automatically sends all rewards the `stash` address, where it gets bonded as an additional stake. This will increase your probability of staying in the `validator` set.

2. `Stash account (do no increase the amount at stake)`

As for 1. this automatically sends all rewards the `stash` address, but does *not* get bonded as stake, meaning you it will not help "guard" your spot in the `validator` set.

3. `Controller account`

This sends all rewards to the `controller`, at your disposal.

#### Validating preferences
1. The `reward commission` is how the (joy) staking rewards are split between yourself and any potential [nominators](#nominating). The default (0) means that the reward is split based on the amount of bonded stake the `validator` and `nominators` have put up. Example:

Let `v` [Joy] be the bonded tokens for the validator `stash`
Let `p` [Joy] be the `payment preference` decided by the validator
Let `n1` [Joy] be the bonded tokens for the nominator1 `stash`
Let `n2` [Joy] be the bonded tokens for the nominator2 `stash`
Let `r` [Joy] be the reward that `era`

```
# payout for the validator
p + (v/(v+n1+n2)*(r-p))
# payout for the nominator1
(n1/(v+n1+n2)*(r-p))
```


## Nominating

If you want to get some return on your tokens without running a node yourself, you can `nominate` another `validator` and get a share of their rewards.

This might also come in handy if there are too many `validators` and you don't have enough tokens get a spot, or if you have to shut down your own node for a while.

#### Generate your keys

1. Go to the [Pioneer App](https://testnet.joystream.org), and select `My keys` in the sidebar. Click the `Create keys` tab.

Names are entirely optional, but the next steps will be easier if you follow the system suggested.

2. For ease of use, name your first keypair "stash", or at least something that contains the word.

If you want to be able to recover your keys later, write down your mnemonic seed, key pair crypto type and secret derivation path.

3. Depending on your browser, you might have to confirm saving the json file.

4. Repeat the process for your "controller" key.

You should now have two sets of keys, namely:
- the "stash" key that will stake your funds
- the "controller" key that you will use to operate your validator

5. If you already have tokens, transfer the bulk to your "stash" account. If you don't yet have any tokens, [click here](https://faucet.joystream.org/). Solve the captcha, and you should receive tokens.

If you want/need more, ask in the telegram chat. Note that long time followers will receive more tokens than newcomers.

6. Send some tokens to your "controller". It needs to perform at least two transactions, but better to send ~10.

#### Configure your validator keys

In order to be a `Nominator`, you need to stake. Note that you may have to refresh your browser if you're not seeing the options right away.

1. In [Pioneer](https://testnet.joystream.org/), click `Validators` in the sidebar, and then the `Account actions` tab.
2. Click the `+ New stake` button, and select the keys from the first two dropdowns.
3. In the third field, enter the amount you want to stake (the maximum amount is the tokens in the account -1).
4. In the bottom dropdown, select the payment destination. Your selection here depends on your preferences.
5. If the transaction goes through, you should now see a `Nominate` button next to your "stash" and "controller" keys in this window. Click it, and select the "stash" account(s) of the `Validator(s)` you want to `Nominate` for.
7. Once submitted, you will start earning a share of the rewards.

---

# Troubleshooting
If you had any issues setting it up, you may find your answer here!
<!---

#### Unstaking

If you stop validating by killing your node before unstaking, you will get slashed and kicked from the `validator` set. If you know in advance (~1hr) you can do the following steps instead:

First, make sure you have set `Fully Featured` interface in the `Settings` sidebar.
1. In `Validator Staking`, click `Stop Validating` with your controller. This can also be done via `Extrinsic`: With `controller` -> `staking` -> `chill()`.

If you are just pausing the `validator` and intend to start it up later, you can stop here. When you are ready to start again, fire up your node, go to `Validator Staking`, and click `Validate`.

If you want to stop being a `validator` and move your tokens to other/better use, continue.

---

2. Next you must unbond. In `Extrinsics`, using the `controller`, select `staking` -> `unbond(value)` and choose how much you want to unbond, `<unbonding>`. Submit Transaction.

At this point, you can just wait 2hrs to be sure, and proceed to step `6.` Or:

---

3. Go to `Chain State` -> `staking` -> `ledger(AccountId): Option<StakingLedger>` with the `controller`. Output:
```
# If you have successfully initiated unstaking:
{"stash":"5YourStashAddress","total":<tot_bonded>,"active":,<act_bonded>:[{"value":<unbonding>,"era":<E_unbonded>}]}
# If you have not successfully initiated unstaking, or it has already completed:
{"stash":"5YourStashAddress","total":<tot_bonded>,"active":,"<act_bonded>":[]}
```
* `<tot_bonded>` Is the total amount you have staked/bonded
* `<act_bonded>` Is the amount of tokens that is not being unlocked
* `<unbonding>` Is the amount of tokens that is in the process of being freed
  * `<unbonding>` + `<act_bonded>` = `<tot_bonded>`
* `<E_unbonded>` Is the `era` when your tokens will be "free" to transfer/bond/vote

The `era` should only change every 600 blocks, but certain events may trigger a new era. To calculate when your funds are "free"
4. In `Chain State` -> `staking` -> `currentEra()`. Let output be `<E_current>`
5. In `Explored` collect `<blocks_in_era>/600` under era.
```
600(<E_unbonded> - <E_current> - 1) - <blocks_in_era> = <blocks_left>
(<blocks_left> * 6)/60 = <minutes_left>
```
After `<minutes_left>` has passed, ie. `<E_current>` = `<E_unbonded>`, your tokens should be free.
Repeat step `3.` if you want to confirm.
```
# If you have completed unstaking:
{"stash":"5YourStashAddress","total":<tot_bonded>,"active":,"<act_bonded>":[]}
```
---

6. In `Extrinsics`, using the `controller`, select `staking` -> `withdrawUnbonded()`

Your tokens should now be "free".

--->
