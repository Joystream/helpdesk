<p align="center"><img src="img/helpdesk-repo.svg"></p>

<div align="center">
  <h4>Guides to get started on our <a href="https://testnet.joystream.org/">current testnet</a> in links below<h4>
</div>

<div align="center">
  <h3>
    <a href="/roles/validators">
      Validators
    </a>
    <span> | </span>
    <a href="/roles/council-members">
      Council Members
    </a>
    <span> | </span>
    <a href="/roles/storage-providers">
      Storage Providers
    </a>
    <span> | </span>
    <a href="/roles/builders">
      Bug Reporters
    </a>
  </h3>
</div>

# Table of Contents

<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
- [Table of Contents](#table-of-contents)
- [Overview](#overview)
- [Contribute](#contribute)
- [Get Paid to Participate](#get-paid-to-participate)
  - [How it Works](#how-it-works)
- [Get Started](#get-started)
  - [Generate Keys](#generate-keys)
  - [Get a Membership](#get-a-membership)
- [Active Roles](#active-roles)
  - [Validators](#validators)
    - [Description](#description)
    - [Incentives](#incentives)
    - [Payouts](#payouts)
  - [Council Members](#council-members)
    - [Description](#description-1)
    - [Incentives](#incentives-1)
    - [Payouts](#payouts-1)
  - [Storage Providers](#storage-providers)
    - [Description](#description-2)
    - [Incentives](#incentives-2)
    - [Payouts](#payouts-2)
  - [Builders and Bug Reporters](#builders-and-bug-reporters)
    - [Description](#description-3)
    - [Incentives](#incentives-3)
    - [Payouts](#payouts-3)
- [Role Coordination](#role-coordination)
    - [Account Linking](#account-linking)
- [Other Features and Future Roles](#other-features-and-future-roles)
  - [Upload Content](#upload-content)
  - [On-Chain Forum](#on-chain-forum)
- [Glossary](#glossary)
<!-- TOC END -->


# Overview
This repo contains detailed guides and help for users to interact with our current [testnet](http://testnet.joystream.org/).

# Contribute
If you find something that is wrong or missing, please make an [Issue](https://github.com/Joystream/helpdesk/issues), or better yet, fork the repo and make a [PR](https://github.com/Joystream/helpdesk/pulls) to help us improve! It might even qualify for a [reward](#builders-and-bug-reporters). For more information on this, please see the [bounties repo](https://github.com/Joystream/bounties).

# Get Paid to Participate
Some of the roles will be compensated in [Monero](https://www.getmonero.org/). Our philosophy behind the choice of paying for participation is outlined in [this](https://blog.joystream.org/pay-for-play/) blog post. Information about the current incentive structure can be found in the list of [Active Roles](#active-roles) below.

## How it Works
**Note**
After introducing `Memberships` to the platform, we found it to be confusing to have a concept of both `Accounts` and `Memberships`. We are in the process of renaming the `Accounts` to the `Keys`, but there are still traces of `Accounts` showing up.

In order for us know what address to pay, you must tie your Joystream address to your monero address. The easiest way to do this is in the `My memo` tab under the `My Keys` sidebar.

```
# Only the part in the line below goes in the memo:
"4or8YourXmrAddressInDoubleQuotesAndNothingElse"
```

For our convenience, we ask you to use a regular address or sub-address (95 char) instead of the (106 char) payment-ID style address. The latter will not be paid out automatically, but if you ask nicely, you might get away with it once.

# Get Started
To get started and participate on the Joystream testnets, you must first generate `Key(s)`, and sign up for a `Membership`. This requires no software or downloads, and can be done in your browser [here](http://testnet.joystream.org).

## Generate Keys
Click `My Keys` in the sidebar, and then select the `Create Keys` tab. The choices you make from here, depends a little on how you want to participate. If you just want to play around, you can just follow the defaults. If you have a specific role in mind, you might want to follow the links to the instructions in the header, or access them via [Active Roles](#active-roles).

In any event, the `Keys` will be stored in your browser for your convenience, but it's safest to save your `Raw seed` (you need it for certain roles) and save the .json file. The `Mnemonic` can also be used to restore your `Keys`, but will not do you any good if you want to become a `Validator`.

## Get a Membership
To become a `Member` of the platform, you need some tokens. Either click the `Free Tokens` link, or click [here](https://testnet.joystream.org/faucet). After you solved the captcha, your tokens should be on their way.

**Note**
All transactions (extrinsics) cost 1 Joy token, so you should always keep a little in reserve, as this also applies to such actions as voting, unstaking, and posting in the new [forum](https://testnet.joystream.org/acropolis/pioneer/#/forum).

Now, click `Members` in the sidebar, and select the `Register` tab. Choose a `Handle/nickname`. Optionally, provide a link to an image file for your avatar, and fill in the markdown enabled `About` field.

# Active Roles

The list below shows the currently active roles available at our current [testnet](https://testnet.joystream.org/pioneer).

## Validators

<p align="center"><img src="img/validator_50.png"></p>

### Description
In proof of stake systems, block producers, or `Validators`, are typically paid a fixed amount for each block produced. `Validators` must run a full node.

A detailed guide to setting up the `Validator` node and settings can be found [here](/roles/validators).

### Incentives
Due to some connectivity issues we had for a while, the `Validator` nodes were often getting booted. Because of this, we are increasing the payout pool from $30 to $50 per week.

```
blocktime = 6
weekly_reward = 5000
seconds_in_week = 60*60*24*7

blockreward = (weekly_reward * blocktime)/seconds_in_week
print(blockreward)

----

0.05
```

The number - 0.05 cents per block - seems a bit underwhelming, but validation requires little effort for the user after setup, and blocks come in every 6 seconds. With armv7 binaries or low-end VPS nodes, it should be cheap to run!

### Payouts
`Validators` must include their [XMR address](#how-it-works) in the `memo` of their `controller` key.

Payouts will be made every Monday at ~11:00GMT.

## Council Members

<p align="center"><img src="img/council_10.png"></p>

### Description

`Council Members` are elected by the stakeholders in the system to act in the interest of their constituency. Currently, `Council Members` can only vote on `proposals` to upgrade the `runtime`. In the future, the council will also allocate the platform's resources, and hire executive personnel to run the day to day operations.

A detailed explanation of the election cycle and responsibilities can be found [here](/roles/council-members).

### Incentives

We are looking at how to best incentivize them to act in the platform's long term interest. As this position generated less interest than we anticipated, we are tweaking the incentives by increasing the payout to get elected from $8 to $10.

If during you term a proposal to upgrade the runtime is submitted by the `sudo` key, `5CJzTaCp5fuqG7NdJQ6oUCwdmFHKichew8w4RZ3zFHM8qSe6` anyone that votes `yes` will receive a bonus worth $10.

### Payouts
During the `Announcement` and `Voting` stage, you should include some information about yourself, and why you should get elected in your `memo` field. If you do get elected, make sure to change the `memo` field to your monero address in order to get your reward.

Payouts will be made at ~11:00GMT the day after the election/vote.

## Storage Providers

<p align="center"><img src="img/storage_300.png"></p>

### Description

You can't have a video platform without videos, so someone has to take the role of storing the data. In the future, this will be a highly specialized role, focusing on what is implied by the name of the role. For Acropolis, it will in practice also entail the future `Bandwidth Provider` role.

Unlike `Validators` that can come and go without too much friction (at least for now), a new `Storage Provider` will currently need to replicate the entire content directory. As a consequence, the platform needs some stability for this role to avoid providing a poor user experience, or worse, loss of data.

### Incentives

Up to 12 `Storage Providers` that keep a full copy and provides continuous service for at least 24h will compete for $360 per week. In addition, you will earn $0.025/GB/week calculated on an average basis. Please note that the setup is a lot more complicated this time, so some experience using Linux on the command line is required. You will also need a domain to point to your node, so unless you already own one (that you don't mind using), you will need to buy one... A detailed guide to setting up the node can be found [here](/roles/storage-providers).

We will try our best to police the `Storage Providers`, so if you are not doing your job (either lack of maintenance or cheating), at least make sure to not get caught!


### Payouts

`Storage Providers` must include their [XMR address](#how-it-works) in the `memo` of their `membership` key, or their `storage` key to qualify for rewards. The former is "better", but requires a little more work...

Payouts will be made every Monday at ~11:00GMT.

## Builders and Bug Reporters

<p align="center""><img src="img/bug-report.png" style="height:400px"></p>

### Description

Unlike the `Validators` and `Council Members`, the bug bounty payments will be somewhat subjective. Long term, such decisions will be resolved by the platform, so in future testnets these payouts will at least partially be made by the Council.

We have recently made a [bounties repo](https://github.com/Joystream/bounties) where you can find specific tasks and their rewards, and we will add more bounties and evolve the system as we grow. In addition to the bounties we propose, we are always looking for suggestions for bounties from the community.

### Incentives

If you find a bug, potential improvement, or just an idea, there are a couple of ways to earn your reward:

#### Report a software bug

Go to the applicable technical repo(s), e.g. [node repo](https://github.com/Joystream/substrate-node-joystream), [Pioneer repo](https://github.com/Joystream/apps/tree/joystream), [storage node repo](https://github.com/Joystream/storage-node-joystream), [runtime-repo](https://github.com/Joystream/substrate-runtime-joystream), etc. and make an `Issue`. You will be compensated based on the importance and "quality", the latter of which is measured from the level of details in general, like how to reproduce, pasted log outputs, etc.

#### Errors in the helpdesk guides (or a non-code repo)

If you find something missing, inaccurate or poorly described, either report an `Issue`, or even better, make a `Pull request`.

This applies equally to this repo as well as the other non-code repos, e.g. [landing repo](https://github.com/Joystream/joystream), [communications repo](https://github.com/Joystream/communications), [bounties repo](https://github.com/Joystream/bounties), etc. it will most likely be covered by [this bounty](https://github.com/Joystream/bounties/issues/3). Note that the bar here is quite low (grammar, dead links, etc.) so more significant findings can lead to significantly larger payouts.

#### Fix a software bug, or add/improve a feature

If you want, you can just make a PR directly, and your contribution will be compensated. If it's an extensive job though, it would be best for all parties if you propose a bounty yourself as outlined [here](https://github.com/Joystream/bounties#proposals). We could then agree on terms in advance, so no one will be left disappointed.

### Payouts

The contributor must include either their Joystream or monero address when submitting the issue/PR. If you choose the former, you must then make sure to add your monero address to the `memo` field of your Joystream address.

# Role Coordination

We have decided to use [Telegram](https://telegram.org/) to allow workers to coordinate with each other.

In the future, communication between actors in our governance system will be managed by an on-chain communication solution. For the moment however, as this chat client does not exist, it is necessary to conduct the communication necessary to perform your role through a third-party application.

We feel that the privacy features of Telegram make it the most effective option for this purpose at the moment, though we are open to suggestions regarding alternatives from members of our community!

There are currently four active chat groups for the Acropolis testnet. We will be adding more groups upon the launch of our Rome testnet (currenly in development).

<img src="img/telegram.jpg" width="400">

#### Currently Active Groups

- Validators ([invite link](example))
- Council Members ([invite link](example))
- Storage Providers ([invite link](example))
- Builders and Bug Reporters ([invite link](example))
- Content Creator _(not yet launched)_
- Content Curator _(not yet launched_

## Account Linking

In order for us and other members of the group to link your Telegram identity to your keys and accounts on our testnet, we will need you to mention your Telegram username within the `memo` of the Pioneer (testnet portal) account you are using to perform your role.

You may want to consider seting up a separate Telegram account from your normal one to avoid your testnet activities being linked to your real-world identity, though this is entirely optional.

# Other Features and Future Roles

This section covers other things you can do after [getting started](#getting-started), that isn't a paid role as of now.

## Upload Content

Since Athens, `members` can upload content. Currently, there are no rewards for doing so, but any user created content is welcome!

## On-Chain Forum

This is the first step in providing users, infrastructure role participants, `Council Members` and future stakeholders a way to communicate and coordinate. Hopefully, this method of interaction will further help develop a strong community around Joystream. Note that you have to be a `member` to post, and only the forum moderator (forum sudo) can create categories.

# Glossary

TODO
