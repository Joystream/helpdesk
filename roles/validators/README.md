<p align="center"><img src="img/validator_new.svg"></p>

<div align="center">
  <h4>This is a step-by-step guide for setting up your <a href="https://github.com/Joystream/substrate-node-joystream">full node</a>, and getting started as a Validator on the latest
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
</div>



Table of Contents
==
<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
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
    - [Stop Validating](#stop-validating)
- [Advanced](#advanced)
  - [Run as a service](#run-as-a-service)
    - [Configure the service](#configure-the-service)
    - [Starting the service](#starting-the-service)
    - [Errors](#errors)
  - [Settings](#settings)
    - [Bonding preferences](#bonding-preferences)
    - [Validating preferences](#validating-preferences)
    - [Example](#example)
  - [Nominating](#nominating)
    - [Generate your keys](#generate-your-keys-1)
    - [Configure your keys](#configure-your-keys)
- [Rewards](#rewards)
  - [Claiming Rewards](#claiming-rewards)
    - [Claiming in Bulk](#claiming-in-bulk)
    - [Claiming one `era` at the Time](#claiming-one-era-at-the-time)
    - [Check claims made](#check-claims-made)
  - [Rewards on Joystream](#rewards-on-joystream)
    - [Dynamic Parameters](#dynamic-parameters)
    - [Fixed Parameters](#fixed-parameters)
    - [Validator set and block production](#validator-set-and-block-production)
    - [Total rewards calculation](#total-rewards-calculation)
    - [Examples](#examples)
- [Slashing](#slashing)
  - [Offline](#offline)
    - [Offline Example](#offline-example)
    - [Offline Slashing Size](#offline-slashing-size)
- [Troubleshooting](#troubleshooting)
  - [Unstaking](#unstaking)
    - [In Pioneer](#in-pioneer)
    - [Using Extrinsics](#using-extrinsics)
<!-- TOC END -->


# Overview

This page contains all information on how to setup your node and becoming a `Validator` on the Joystream Testnets. It will be updated for improvements, and when something changes for new testnets.

If you want to earn more `tJOY` tokens, but for some reason can't or won't become a `Validator`, you can [`Nominate`](#nominating) instead.

# Instructions

The instructions below cover Mac and Linux (64 bit and armv7). Windows binaries are currently not available.

**Note**
If you are just running a node, and don't want to be a `Validator`, you can skip the flags
`--pruning archive` and `--validator`


# On Your Machine

---

## Mac

* Every time something is written in `<brackets>`, it means you have to replace this with your input, without the `<>`.
* When something is written in `"double_quotes"`, it means the number/data will vary depending on your node or the current state of the blockchain.
* For terminal commands, `$` means you must type what comes afterwards. `#` Means it's just a comment/explanation, and must not be typed.
```
# This is just a comment, don't type or paste it in your terminal!
$ cd ~/
# Only type/paste the "cd ~/, not the preceding $ !
```
### Setup Node

Open the terminal (Applications->Utilities):

```
$ cd ~/
$ wget https://github.com/Joystream/joystream/releases/download/v7.5.0/joystream-node-3.3.0-fdb75f5ec-x86_64-macos.tar.gz
$ wget https://github.com/Joystream/joystream/releases/download/v7.5.0/joy-testnet-4.json
----
# If you don't have wget installed, paste the link in your browser save.
# Assuming it gets saved in your ~/Downloads folder:
$ mv ~/Downloads/joystream-node-3.3.0-fdb75f5ec-x86_64-macos.tar.gz ~/
---
$ tar -vzxf joystream-node-3.3.0-fdb75f5ec-x86_64-macos.tar.gz
$ ./joystream-node --chain joy-testnet-4.json --pruning archive --validator
```
- If you want your node to have a non-random identifier, add the flag `--name <nodename>`
- If you want to get a more verbose log output, add the flag `<nodename> --log runtime`

Your node should now start syncing the blockchain. The output should look like this:
```
Joystream Node
  version "Version"-"your_OS"
  by Joystream, 2019-2020
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

### Keys

Now you need to generate your keys. Go [here](#generate-your-keys) to do that now.

### Final Step

Now it's time to configure your keys to start validating. Go [here](#configure-your-validator-keys) to configure your `Validator`.

---

## Linux

* Every time something is written in `<brackets>`, this means you have to replace this with your input, without the `<>`.
* When something is written in `"double_quotes"`, it means the number/data will vary depending on your node or the current state of the blockchain.
* For terminal commands:
  * `$` means you must type what comes afterwards
  * `#` Means it's just a comment/explanation for the readers convenience
```
# This is just a comment, don't type or paste it in your terminal!
$ cd ~/
# Only type/paste the "cd ~/, not the preceding $ !
```
### Setup Node

Open the terminal:

```
$ cd ~/
# 64 bit debian based Linux
$ wget https://github.com/Joystream/joystream/releases/download/v7.5.0/joystream-node-3.3.0-fdb75f5ec-x86_64-linux-gnu.tar.gz
$ tar -vzxf joystream-node-3.3.0-fdb75f5ec-x86_64-linux-gnu.tar.gz
# armv7 (eg. raspberry pi)
$ wget https://github.com/Joystream/joystream/releases/download/v7.5.0/joystream-node-3.3.1-arm-v7.tar.gz
$ tar -vzxf joystream-node-3.3.1-arm-v7.tar.gz
# For both
$ wget https://github.com/Joystream/joystream/releases/download/v7.5.0/joy-testnet-4.json
$ $ ./joystream-node --chain joy-testnet-4.json --pruning archive --validator
```
- If you want your node to have a non-random identifier, add the flag `--name <nodename>`
- If you want to get a more verbose log output, add the flag `<nodename> --log runtime`

Your node should now start syncing the blockchain. The output should look like this:
```
Joystream Node
  version "Version"-"your_OS"
  by Joystream contributors, 2019-2020
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

### Keys

Now you need to generate your keys. Go [here](#generate-your-keys) to do that now.

### Final Step

Now it's time to configure your keys to start validating. Go [here](#configure-your-validator-keys) to configure your `Validator`.

---

# In the Pioneer app (browser)

## Validator Setup

### Generate your keys

While the node is syncing, you can start the process of setting up the rest.

1. Go to the [Pioneer App](https://testnet.joystream.org/), and select `My Keys` in the sidebar. Click the `Add account` button.

Names are entirely optional, but the next steps will be easier if you follow the system suggested.

2. For ease of use, name your first keypair "stash", or at least something that contains the word.

If you want to be able to recover your keys later, write down your mnemonic seed, key pair crypto type and secret derivation path.

3. Depending on your browser, you might have to confirm saving the json file.

4. Repeat the process for your "controller" key.

You should now have two sets of keys, namely:
- the "stash" key that will stake your funds
- the "controller" key that you will use to operate your validator

5. If you already have tokens, transfer the bulk to your "stash" account. If you don't yet have any tokens, ask in the [Discord chat](https://discord.gg/DE9UN3YpRP), and you shall receive :)

6. Send at least 1 token to your "controller".

### Configure your validator keys

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

2. Back in [Pioneer](testnet.joystream.org/), click `Validators` in the sidebar, and then the `Account actions` tab.
3. Click the `+ Stash` button, and select the keys from the first two dropdowns.
4. In the third field, enter the amount you want to stake (the maximum amount is the tokens in the account -1).
5. In the bottom dropdown, select the payment destination. Your selection here depends on your [preferences](#bonding-preferences).
6. If the transaction goes through, you should now see a `Set Session Key` button next to your "stash" and "controller" keys in this window. Click it, paste in your `0xa0very0long0hex0string` in the field, and confirm.
7. If the transaction goes through, you should now see a `Validate` button instead. Click it, and set your `reward commission percentage`, a number between 0 and 100. Your input here depends on your preferences. A "high" number means you are less likely to get [Nominators](#nominating).

Refresh your browser, and select the `Waiting` tab. If your account shows under `intentions`, wait for the next `era`, and you will be moved to the `validators` list (in the `Staking Overview` tab).

### Stop Validating
Unless you want to risk getting slashed, you need to "gracefully" stop validating.
This can be done easily in [Pioneer](testnet.joystream.org/)
1. Click `Validators` in the sidebar, then choose the `Account actions` tab.
2. Click the "Stop" button to the right, and confirm.
3. Once you are dropped from the Validator set (can take up to 70min), you can safely stop your node.

# Advanced

## Run as a service

If you are running your node on a [Linux](#linux) and want to run it as a [service](https://wiki.debian.org/systemd/Services), you can set it up this way.
Note that you should avoid this unless you know what you are doing, are running your node on **your own VPS** or a single board computer. With great (sudo) privileges, comes great responsibilities!

If you are already running as a `validator`, consider [unstaking](#unstaking) first, as you may experience some downtime if you make any mistakes in the setup.

### Configure the service

Either as root, or a user with sudo privileges. If the latter, add `sudo` before commands.

```
$ cd /etc/systemd/system
# you can choose whatever name you like, but the name has to end with .service
$ touch joystream-node.service
# open the file with your favorite editor (I use nano below)
$ nano joystream-node.service
```

#### Example with user joystream

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
        --chain joy-testnet-4.json \
        --pruning archive \
        --validator \
        --name <nodename>
Restart=on-failure
RestartSec=3
LimitNOFILE=8192

[Install]
WantedBy=multi-user.target
```

#### Example as root

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
        --chain joy-testnet-4.json \
        --pruning archive \
        --validator \
        --name <nodename>
Restart=on-failure
RestartSec=3
LimitNOFILE=8192

[Install]
WantedBy=multi-user.target
```

### Starting the service

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

### Errors

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

### Bonding preferences
The bonding preferences decide on how your (tJOY) staking rewards are distributed. There are three alternatives:
1. `Stash account (increase the amount at stake)` (default).

This automatically sends all rewards the `stash` address, where it gets bonded as additional stake. This will increase your probability of staying in the `validator` set.

2. `Stash account (do no increase the amount at stake)`

As for 1. this automatically sends all rewards the `stash` address, but does *not* get bonded as stake, meaning you it will not help "guard" your spot in the `validator` set.

3. `Controller account`

This sends all rewards to the `controller`, at your disposal.

### Validating preferences
The `reward commission` determines how the (tJOY) staking rewards are split between yourself and any potential [nominators](#nominating). The default - 0(%) - means that the reward is split based on the amount of bonded stake the `validator` and `nominators` have put up. Example:

- Let `v` be the bonded tokens by the validators `stash` key
- Let `c` be the `reward commission` decided by the validator
- Let `n1` be the bonded tokens by the nominator1 `stash`
- Let `n2` be the bonded tokens by the nominator2 `stash`
- Let `r` be the reward for the individual validators that `era`

```
# payout for the validator
c*r + r*(1 - c)*v/(v + n1 + n2)
# payout for the nominator1
r(1 - c) * n1/(v + n1 + n2)
```

### Example
- assume there are 10 active validators in this era
- validator 1 bonds 100,000 tJOY
- validators 2-10 all bonds 300,000tJOY
- validator 1 has `reward commission` set to 10%
- nominator A bonds 100,000 tJOY, and nominates validator 1
- nominator B bonds 50,000 tJOY, and nominates validator 1
- thus, validator A has an effective stake of 250,000 tJOY
- after the end of the era, the total rewards are 25,000 tJOY

```
# All validators gets an equal share, before sharing with nominators:
R_v = 25,000tJOY / 10 = 2,500tJOY

# payout for validator 1
R_v.1 = 0.1 * 2,500tJOY + 2,500tJOY *(1 - 0.1) * (100,000tJOY / 250,000tJOY) = 1,150tJOY

# payout for nominator A
R_n.A = 2,500tJOY *(1 - 0.1) * (100,000tJOY / 250,000tJOY) = 900tJOY

# payout for nominator B
R_n.B = 2,500tJOY *(1 - 0.1) * (50,000tJOY / 250,000tJOY) = 450tJOY
```

As the Validator carries the cost of operating and maintaining their nodes, it makes sense for them to take a slice of the pie before sharing.

## Nominating

If you want to get some return on your tokens without running a node yourself, you can `nominate` another `validator` and get a share of their rewards.

This might also come in handy if there are too many `validators` and you don't have enough tokens get a spot, or if you have to shut down your own node for a while.

### Generate your keys

1. Go to the [Pioneer App](https://testnet.joystream.org/), and select `My keys` in the sidebar. Click the `Add account` button.

Names are entirely optional, but the next steps will be easier if you follow the system suggested.

2. For ease of use, name your first keypair "stash", or at least something that contains the word.

If you want to be able to recover your keys later, write down your mnemonic seed, key pair crypto type and secret derivation path.

3. Depending on your browser, you might have to confirm saving the json file.

4. Repeat the process for your "controller" key.

You should now have two sets of keys, namely:
- the "stash" key that will stake your funds
- the "controller" key that you will use to operate your validator

5. If you already have tokens, transfer the bulk to your "stash" account. If you don't yet have any tokens, ask in the [Discord chat](https://discord.gg/DE9UN3YpRP), and you shall receive :)

6. Send at least 1 token to your "controller".

### Configure your keys

In order to be a `Nominator`, you need to stake. Note that you may have to refresh your browser if you're not seeing the options right away.

1. In [Pioneer](testnet.joystream.org/), click `Validators` in the sidebar, and then the `Account actions` tab.
2. Click the `+ Stash` button, and select the keys from the first two dropdowns.
3. In the third field, enter the amount you want to stake (the maximum amount is the tokens in the account -1).
4. In the bottom dropdown, select the payment destination. Your selection here depends on your [preferences](#bonding-preferences).
5. If the transaction goes through, you should now see a `Nominate` button next to your "stash" and "controller" keys in this window. Click it, and select the "stash" account(s) of the `Validator(s)` you want to `Nominate` for.
7. Once submitted, you will start earning a share of the rewards.

# Rewards
Rewards are the most critical part of any blockchains infrastructure, block production, whether it's from [Proof of Work](https://en.wikipedia.org/wiki/Proof_of_work) (using miners, e.g. Bitcoin)  or [Proof of Stake](https://en.wikipedia.org/wiki/Proof_of_stake) (using validators, like Joystream). Validators are rewarded for producing, propagating and securing the network.

## Claiming Rewards
Rewards are no longer paid out automatically to the validators, and it must be done manually.
We have made it so you have ~2 weeks to claim your rewards, but after that, they can no longer be claimed.

This was not a voluntary decision from Jsgenesis, but part of the new staking module from [Substrate](https://github.com/paritytech/substrate). The reason is simply that if your validator set is very large and with a lot of nominators (which will be the case for many Substrate based chains), every payout would require a lot of transactions. By instead making it manual, this will be spaced out.

**Note:**
Claiming rewards for a specific Validator can be done by anyone, not just the Validator themselves. However, only the Validator (and Nominator) can batch up multiple claims in one [bulk](#claiming-in-bulk).

### Claiming in Bulk
This can only be done if you have the keys for the Validator or Nominator you want to claim for:
In the UI, Validators can claim rewards in "bulks" of 40 `eras` at the time:
1. In [Pioneer](testnet.joystream.org/), click `Validators` in the sidebar, and then the `Payouts` tab
2. Make sure the `Max, x eras` are selected
3. At the bottom of the page, all your you will see an overview of:
  - which `eras` you can claim rewards for
  - the total amount `available` you are "owed"
  - the time `remaining` to claim (your "oldest") reward
4. Click the `Payout` button at the right end of the row, and confirm to claim the "oldest" 40 `era` rewards for you, and any potential [Nominators](#nominating) that has claim to some of your rewards
5. If you have more than 40 `eras`, you can repeat this after the first transaction is complete

**Note:**
- If a Validator had any Nominator(s) in the `eras` for which they claim rewards, the Nominator(s) will automatically get their rewards for said `eras`
- A Nominator that claims rewards for multiple `eras`, the Validator(s) they nominated in said `eras` will automatically also get their rewards.

### Claiming one `era` at the Time
This can be done by *any* account:
1. Go to the [extrinsics](https://testnet.joystream.org/#/extrinsics) tab
2. Select `staking.payoutStakers(validator_stash, era)`
3. Select/paste the address of the `stash` account you want to claim on behalf of/for
4. Type in the `era` you want to claim for, and submit

### Check claims made
To find out if a "stash" have claimed reward(s) from `era(s)`:
- [chain state](https://testnet.joystream.org/#/chainstate) query of `ledger(AccountId): Option<StakingLedger>` with the *any* current, or "historic" controller. Output:
```
{
  stash: 5YourStashAddress,
  total: <tot_bonded> JOY,
  active: <act_bonded> JOY,
  unlocking: [],
  claimedRewards: [
    <era_a>,
    <era_b>,
    ...
    <era_i>,
  ]
}
```
**Note:**
To understand what `unlocking` means, go [here](#using-extrinsics).

## Rewards on Joystream
For Substrate based blockchains, the validator rewards depends on some [dynamic parameters](#dynamic-parameters), that will change continuously, and some [fixed parameters](#fixed-parameters) in the chain spec.

### Dynamic Parameters
1. Active validators (`V_a`) - the number of `validators` currently running. This can be found:
  - in the [Validators](https://testnet.joystream.org/#/staking) tab -> validator (**`V_a`** / `V_i`)
  - or through a [chain state](https://testnet.joystream.org/#/chainstate) query of `session.validators()` (and count them)
2. Max/Ideal validators `V_i` - the max number of active validators. This number can be changed through proposals, but was initially set to 20. Current value can be found:
  - in the [Validators](https://testnet.joystream.org/#/staking) tab -> validator (`V_a` / **`V_i`**)
  - or through a [chain state](https://testnet.joystream.org/#/chainstate) query of `staking.validatorCount()`
3. Issuance `I` - total tJOY tokens in circulation. This can be found:
  - in the [explorer](https://testnet.joystream.org/#/explorer) tab
  - or through a [chain state](https://testnet.joystream.org/#/chainstate) query of `balances.totalIssuance()`
4. Validator stake (`S_v`) - ie. the total stake of the `validators` set, corresponding to the sum of the stakes of each `validator`, plus the stake of their [nominators](#nominating) if any. This can be found:
  - in the [staking](https://testnet.joystream.org/#/staking/targets) tab (alongside `I`, and the percentage of `S_v / I` - also known as the Active staking ratio, `S_v,ar`, see 5.)
  - or through a [chain state](https://testnet.joystream.org/#/chainstate) query of `staking.erasTotalStake(<EraIndex>)`
    - the `<EraIndex>` can be found by `staking.activeEra()`
5. Active staking ratio, `S_v,ar` - the current ratio of tokens staked by active validators (and their nominators) and the issuance. So `S_v,ar = S_v / I`

### Fixed Parameters
6. Minimum inflation, `I_min` - the min yearly inflation distributed to validators.
  - This number is currently set to `5%`.
7. Maximum inflation, `I_max` - the max yearly inflation distributed to validators.
  - This number is currently set to `75%`.
8. Ideal staking ratio, `S_v,ir` - the ideal ratio of effective stake over issuance for maximum validator rewards.
  - This number is currently set to `25%`.
9. Falloff, `F_v` - how quickly the validator rewards drop when the actual staking rate `S_v,ar` exceeds the ideal staking rate `S_v,ir`.
  - This number is currently set to `5%`.
10. Sessions, `session_l` - each `session` (or `epoch`) should last ~10 minutes / 100 blocks `*`
11. Era length, `era_l` - each `era` lasts 60 minutes should last 6 `sessions` -> ~60 minutes / 600 blocks `*`

- `*` For a variety of reasons (such as latency, validators going down, etc.) an `era` can be as little as 1 `session` and a `session` can be a lot fewer blocks than 100.

### Validator set and block production
At the end of each era, a new set of active validators `V_a` is determined by sorting all those that have declared their intention (eg. both the active and next up) by their stake, and selecting up to `V_i` in a descending order.

Those selected are treated as equals, and will have the same chance of being selected to produce blocks and thus get an equal share of the rewards. Slashes however, are applied as a percentage of stake, so a validator with more stake risks getting slashed more despite earning the same.

### Total rewards calculation
As shown, the maximum total validator reward per year is 75% for `S_v,ar = S_v,ir = 0.25`. With an era length of 600 blocks, each era, the maximum total, `R_vm,te` and individual, `R_vm,ie` reward for the validators are:

**Note**
For all calculations, we assume there are (365.2425×24×60×60s)/year.

```
R_vm,te = I * I_max * era_l / year
= I * 0.75 * 3600s / (31556952s)
= 0.0000855596*I

R_vm,ie = R_vm,te / V_a
= 0.0000342238*I/V_a
```

For `S_v,ar<S_v,ir`, the total rewards drop linearly down to the minimum inflation rate `I_min` for `S_v,ar = 0`
For `S_v,ar>S_v,ir`, the total rewards drop exponentially down to the minimum inflation rate for `I_min` `S_v,ar = 1` .

The exact formulae:
```
R_v,te = I * (I_min + (I_max - I_min) * 2^((S_v,ir − S_v,ar) / F_v)) * era_l / year
```

### Examples

The tJOY rewards for the validators can be calculated using this [spreadsheet](https://docs.google.com/spreadsheets/d/13Bf7VQ7-W4CEdTQ5LQQWWC7ef3qDU4qRKbnsYtgibGU/edit?usp=sharing). The examples below should assist in using it:

#### Example A
In addition to the fixed parameters above, suppose:
```
V_a = 20
I = 100,000,000tJOY
S_v = 25,000,000tJOY
```

As `S_v / I = 0.25`, meaning `S_v,ar = S_v,ir` the maximum yearly inflation rate `I_max = 75%` will be shared among the validators. Each era, the total, `R_v,te` and individual, `R_v,ie` reward for the validators are:

----
```
R_v,te = I * I_max * era / year
= 100,000,000tJOY * 0.75 * 3600s / (31556952s)
= 8,556tJOY

R_v,ie = R_v,te / V_a
= 8,556tJOY / 20
= 428tJOY
```

#### Example B
In addition to the fixed parameters above, suppose:
```
V_a = 20
I = 100,000,000tJOY
S_v = 20,000,000tJOY
```

With `S_v / I = 0.2`. Each era, the total, `R_v,te` and individual, `R_v,ie` reward for the validators are:

```
R_v,te = I * (I_min + (I_max - I_min) * S_v,ar / S_v,ir) * era_i / year
= 6,959tJOY

R_v,ie = R_v,te / V_a
= 6,959tJOY / 20
= 348tJOY
```

#### Example C
In addition to the fixed parameters above, suppose:
```
V_a = 20
I = 100,000,000tJOY
S_v = 30,000,000tJOY
```

With `S_v,t=S_v,eff/I=0.3`. Each era, the total, `R_v,te` and individual, `R_v,ie` reward for the validators are:

```
R_v,te = I * (I_min + (I_max - I_min) * 2^((S_v,ir − S_v,ar) / F_v)) * era_l / year
= 4,563tJOY

R_v,ie = R_v,te / V_a
= 4,563tJOY / 20
= 228tJOY
```
#### Example conclusion
As seen above, the difference from staking 5% more or less than the ideal, is quite substantial.

- By staking 5% less, the "loss" is only 18% (6,959tJOY vs 8,556tJOY)
- By staking 5% more, the "loss" is instead 47% (4,563tJOY vs 8,556tJOY)

More information on the staking, rewards and slashing mechanics can be found on the Web3 Foundation's research papers [here](https://research.web3.foundation/en/latest/polkadot/economics/1-token-economics.html).

# Slashing
Just as the Validators are rewarded for producing, propagating and securing the network, they are punished for misbehaving. The slashing mechanics are more complex, so it will not be covered as detailed as the [rewards](#rewards).

Although there are other reasons for getting slashed as a Validator, the reasons that stem from intentional malicious behavior will not be covered here. If you want to learn more about the details of slashing, visit this guide from the [Polkadot](https://github.com/paritytech/polkadot) wiki guide on [slashing (and staking)](https://wiki.polkadot.network/docs/en/learn-staking#slashing).

## Offline
The most likely reason a Validator will get slashed is for going offline without first [stopping](#stop-validating) gracefully.

If `n` Validators go offline, there will be an two "events" at the end of that `session`:
1. `imOnline:SomeOffline`
2. `offences.Offence`

### Offline Example
Suppose we have two Validators offline, - `v_0` and `v_1`. `v_1` has one nominator `n_1` (all `accountId`/address of their "stash"):
By selecting the block the event occured in the [explorer](https://testnet.joystream.org/#/explorer), it will appear like so:

**1** `imOnline:SomeOffline`:
```
At the end of the session, at least one validator was found to be offline.
  Vec<IdentificationTuple>

    0: IdentificationTuple: IdentificationTuple
    [
      <v_0>,
      {
        total: <v_0 stake> JOY,
        own: <v_0 stake> JOY,
        others: []
      }
    ]

    1: IdentificationTuple: IdentificationTuple
    [
      <v_1>,
      {
        total: <v_1+n_1 stake> JOY,
        own: <v_1> JOY,
        others: [
          {
            who: <n_1>,
            value: <n_1 stake> JOY,
          }
        ]
      }
    ]
```
This identities which valididators are reported "offline".


**2** `offences.Offence`:
```
There is an offence reported of the given `kind` happened at the `session_index` and (kind-specific) time slot. This event is not deposited for duplicate slashes. last element indicates of the offence was applied (true) or queued (false).

  Kind
  im-online:offlin

  OpaqueTimeSlot
  0xsomething

  bool
  <Yes> or <No>
```
The key here is whether `bool` is `Yes` (`true`) or `No` (`false`).
- If `Yes/true`, this means a slash will be applied.
- If `No/false`, this means no slash will be applied.

### Offline Slashing Size
The magnitude of the slash (and whether one will be applied at all), depends on the max number of Validator slots allowed (`V_max`), and the number of Validators reported offline `V_off`.
- If `V_off / V_max` < 1/10
  - No slash will be applied
- If `V_off / V_max` > 1/3
  - A max slash of 7% is initiated `*`

The exact formula, from the comment in the codebase, is presented below (with variables changed for clarity):
```
		// the formula is min((3 * (V_off - (V_max / 10 + 1))) / V_max, 1) * 0.07
		// basically, 10% can be offline with no slash, but after that, it linearly climbs up to 7%
		// when 13/30 are offline (around 5% when 1/3 are offline).
```

`*` A single `Offence` adds an entry to the Validators `slash span`. The actual slashing (burning) of tokens will happen ~24h hours later. For more info, we again refer to the [Polkadot Wiki](https://wiki.polkadot.network/docs/en/learn-staking#slashing-across-eras)

---

# Troubleshooting
If you had any issues setting it up, you may find your answer here!

## Unstaking
Due to an unfortunate error in Pioneer which we are working to fix, unstaking requires either lots of patience, or using the chain state/extrinsics tab for certain tasks:

### In Pioneer

If you stop validating by killing your node before unstaking, you will get slashed and kicked from the `Validator` set. If you know in advance (it can take up to 70min) you can do the following steps instead:

1. In `Validator -> Account Actions`, click `Stop`.

If you are just pausing the `validator` and intend to start it up later, you can stop here. When you are ready to start again, fire up your node, go to `Validator Staking`, and click `Validate`.

If you want to stop being a `validator` and move your tokens to other/better use, continue.

---

2. Next you must unbond. In the same window (`Validator -> Account Actions`), next to your keypair, click the rightmost triple dotted "settings" button, select `Unbond funds`, and choose the amount you wish to unbond.

After the transaction has gone through, you will see a new line appearing in the `bonded` column, showing the amount and a "clock" icon. Hovering over this with your cursor will tell you when your unbonding is complete ( starts at <24h / <14,400 blocks), and you can go to the third and final step.

3. Within 24h, the tokens should be unbonded, and you will see a new line appearing in the `bonded` column, showing the amount you can claim and a blue "lock" button. Click the button to finalize the unbonding, and your tokens will be "free" to spend from your "stash".

**Notes:**
- If you have performed multiple unbondings, in different `eras`:
  - hovering over the "clock" will show multiple entries, eg. `<amount>, <time_left>, <block_left>`
  - you may also have both the "clock" and "lock" button, if some of your unbondings are completed
  - if you have any pending [slashes](#slashing), these will be deducted when you perform step 3.


### Using Extrinsics

First, make sure you have set `Fully Featured` interface in the `Settings` sidebar.

#### Definitions
- `<tot_bonded>` Is the total amount you have staked/bonded
- `<act_bonded>` Is the amount of tokens that is not being unlocked
- `<unbonding_n>` Is the amount of tokens that is in the process of being freed from your `n`th `Unbond funds` request  
  - `sum <unbonding_n>` + `<act_bonded>` = `<tot_bonded>`
- `<era_unbonded_n>` Is the `era` when your `n`th `Unbond funds` request tokens will be "free" to transfer/bond/vote

To find out if you have started/completed your `n` unbonding(s):
1. [chain state](https://testnet.joystream.org/#/chainstate) query of `ledger(AccountId): Option<StakingLedger>` with the controller. Output:
```
# If you have successfully initiated unbonding, but the tokens are not unlocked:
{
  stash: 5YourStashAddress,
  total: <tot_bonded> JOY,
  active: <act_bonded> JOY,
  unlocking: [
    {
      value: <unbonding_0> JOY,
      era: <era_unbonded_0>
    },
    {
      value: <unbonding_1> JOY,
      era: <era_unbonded_1>
    },
    ...
    {
      value: <unbonding_n> JOY,
      era: <era_unbonded_n>
    }
  ],
  claimedRewards: [
    <era_a>,
    <era_b>,
    ...
    <era_i>,
  ]
}
```
**Note:**
To understand what `claimedRewards` means, go [here](#check-claims-made).


2. The `era` should only change every 600 blocks, but certain events may trigger a new era. To calculate when your funds are "free" In `Chain State` -> `staking.currentEra()`. Let output be `<era_current>`

If `<era_unbonded_n>` >= `<era_current_n>`, you can claim the unbonded funds in step 3..

3. Once the unbonding is complete, go to [extrinsics](https://testnet.joystream.org/#/extrinsics), with the `controller`, select `staking.withdrawUnbonded(num_slashing_spans)`

**Note:** If you have any "pending" slashes, this will require some more [chain state](https://testnet.joystream.org/#/chainstate) queries, to find the input `num_slashing_spans`.

Your tokens will be "free" to spend from your "stash".
