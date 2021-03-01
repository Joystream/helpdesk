<p align="center"><img src="img/content-curators.svg"></p>

<div align="center">
  <h4>This is a guide for applying, and working as a Content Curator on the latest
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
  <h4>If you are interested in the Content Curator Lead role, please instead visit this
    <a href="../content-curator-lead">dedicated guide</a>.<h4>
</div>



Table of Contents
==
<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
- [Overview](#overview)
- [Hiring Process](#hiring-process)
  - [Applying for a Role](#applying-for-a-role)
    - [Accepting applications](#accepting-applications)
      - [Track the status of your application](#track-the-status-of-your-application)
      - [Withdraw or change your application](#withdraw-or-change-your-application)
    - [Applications in review](#applications-in-review)
      - [Track the status of your application](#track-the-status-of-your-application-1)
  - [Hiring complete](#hiring-complete)
- [Working as a curator](#working-as-a-curator)
  - [Rules](#rules)
    - [Content](#content)
    - [Channels](#channels)
    - [Discretion](#discretion)
  - [Curation](#curation)
    - [Censoring](#censoring)
    - [Updating](#updating)
    - [Removing](#removing)
<!-- TOC END -->

# Overview

This page will contain all information on how to apply for the role of `Content Curator`, and how to perform the various tasks required for the job.

# Hiring Process

First, open [Pioneer](https://testnet.joystream.org/), and navigate to the `Working groups` sidebar. Here you will find an overview of the current `Content Curators`, and the `Content Lead`. In the `Opportunities` tab, you can get an overview of future, current and previous openings, along with terms, settings, status, and history (if applicable). The terms and settings include the following parameters to consider:

- `Max active applicants` - The maximum number of active applicants for an opening
- `Max review period length` - The maximum length (in blocks) of the review period
- `Application staking policy` - This stake applies for the application only
  - A fixed or minimum stake for the application
  - The length (in blocks) from an application has been resolved until the stake is returned
- `Role staking policy` - This stake applies for the role itself, and successful applicants will have these funds locked while being in the role
  - A fixed or minimum stake for the role
  - The length (in blocks) from an unsuccessful application has been resolved, or a successful applicant has quit or gotten fired, until the stake is returned
- `Reward policy` - The rewards (in `X [JOY]/N [blocks]`) for successful applicants


## Applying for a Role

In order to be able to successfully apply for a role as a `Content Curator`, you have to register a membership, which requires tokens. It should also be expected that there will be staking requirements, which will require more tokens. The exact terms should be clear from the listing.

You will be able to complete the application process as long as you have generated a keypair, but your application transaction will be discarded by the runtime for a variety of reasons:
- If you are not a member.
- If you attempt to apply twice with the same `MemberId`.
- If you attempt to apply with an insufficient stake.
- If you try to stake more tokens than you can (note the application transaction costs 1 JOY)
- If you apply for a role with a maximum number of slots, with fixed or no stake requirements, and the maximum application slots have been reached.
- If you try to apply manually through the `Extrinsics` sidebar, you can fail for a variety of other reasons.

### Accepting applications

Only openings in the "Accepting applications" stage can be applied for. Assuming there is one or more openings in this stage that is of interest (and you have sufficient tokens) you can apply for the role. Click the green `APPLY NOW` button inside the Opening box, and follow the staking instructions and write the requested information.

After you have completed this, you will be sent to a confirmation page, where you can submit the application. Once you click `Make transaction and submit application`, a new key will be generated for you. This will be the `controller` key for the role, which you will need to use for all curation transactions if you are hired. It will by default not have a password, and be named `<TITLE OF JOB OPENING> ROLE KEY`. You can rename, set a password, and download a backup .json file of this key in the `My Keys` sidebar.

#### Track the status of your application
Once your application is submitted, you can check the status of your application by selecting this key, and navigate to the `My roles` tab under the `Working groups` sidebar.

#### Withdraw or change your application
While the opening is in the "Accepting applications", you can withdraw your application. As you can not apply twice with the same membership key, the only way to change your application, either to add more stake or update the application text, you need to withdraw your application first. This can be done by selecting the generated role key, navigate to the `My roles` tab under the `Working groups` sidebar, and clicking the `Cancel and withdraw stake` button.

### Applications in review

Once the `Content Curator Lead` is satisfied with the quality/quantity of the applications, the `Applications in review` stage will begin. In this stage, applicants can no longer withdraw their application. The `Content Curator Lead` can do a final review of the applicants, and will make a decision on how many and whom, if any, to hire for the role. As there is a `Max review period length`, inaction will default to no hires, and both the "Role stake" and "Application stake" will be returned in due time.

#### Track the status of your application
As in the [Accepting applications](#accepting-applications) stage, you can track the status of your application by selecting the role key, and navigate to the `My roles` tab under the `Working groups` sidebar.

## Hiring complete

Assuming the `Content Curator Lead` decides to hire one or more applicants, a transaction that hires a set of applicants and sets the `Reward policy` will be made. Successful applicants will appear in the `Workings groups` tab with their membership handle, their "Role stake" and, as time goes, the tokens earned for the job.

Once either the above happens, the lead chooses to terminate the opening without hiring anyone, or the `Max review period length` expires, the opening will go to the `Hiring complete` stage.

As in the previous stages, regardless if your application was successful or not, you can check the status of your application by selecting the role key, and navigate to the `My roles` tab under the `Working groups` sidebar.

If your application was successful, you will now be able to curate content on the Joystream platform.

# Working as a curator

The main job for curators is to regularly check the content directory and channels, and checking that rules and guidelines are being followed.

## Rules
The basic rules are stated below.

### Content

Curators are responsible for ensuring the following:
1. Content is not in violation of the platform [ToS](https://testnet.joystream.org/#/pages/tos), meaning
  - illicit content should be `censored`, and marked for a takedown
  - content must be given assigned the appropriate license and, if required, attribution
  - explicit content must be marked as such
2. Content is resolving and playing as intended
  - content that is not playable should be marked as unlisted, and a heads up should be given to the channel owner in the forum
3. Metadata is correct
  - incorrect metadata should be corrected, unless the mistake requires more severe consequences (see 1.)

### Channels
Channels should be treated the same way as content, and the following basic rules should be enforced:
- Channels that consistently violate the rules for [content](#content), should be censored.

### Discretion

These rules are not clearly defined in all cases, so it's important that curators are able to use discretion. In many cases, it's preferable to try and get in touch with the channel owner first, rather than immediately pull the trigger. If in doubt, contact the `Lead` first. In other cases, immediate action may be required.

"Speak softly, and carry a big stick"
- Theodore Roosevelt

## Curation
Curation can mean either censoring, updating or altogether removing content. It can also involve putting content in a "featured" state on the platform.

A key part of understanding Curation is to understand the basics of the Content Directory using the [CLI](https://github.com/Joystream/joystream/tree/master/cli). Examples:

```
# Info about a specific class:
$ joystream-cli content-directory:class <CLASSNAME|CLASSID>

# Info about a specific entity:
$ joystream-cli content-directory:entity <ENTITYID>

# List all classes:
$ joystream-cli content-directory:classes

# List all entities in a class:
$ joystream-cli content-directory:entities <CLASSNAME|CLASSID>
```

### Censoring
The first step to perform if a video or channel is not in line with the testnet Terms of Service is to censor it.

If the Curator has "Maintainer" permission for a Channel or Video, this is done by the following [CLI](https://github.com/Joystream/joystream/tree/master/cli) command `joystream-cli media:curateContent`. Suppose you want to censor a Video with `entityId` 300:
```
$ joystream-cli media:curateContent --className 10 --status Censored --id 300
```

If it's a minor issue, you can try to reach out to the creator, and have them make the modification required. If the issue gets resolved, you can reverse the censoring by:

```
$ joystream-cli media:curateContent --className 10 --status Accepted --id 300
```

If it's a more serious infraction, contact the Lead and let them know. In general, it's preferable to share the information with other curators regardless.

### Updating
If you have the permission, you can update a Channel (with `entityId` 100) or Video (with `entityId` 200) like so:
```
$ joystream-cli media:updateChannel 100 --asCurator
$ joystream-cli media:updateVideo 200 --asCurator
```
This is particularly useful if the Channel owner is using the wrong "License", or has forgotten "Attribution".


### Removing
If you have the permission, you can remove a Channel (with `entityId` 100) like so:
```
$ joystream-cli content-directory:removeEntity 100 --context <Curator|Lead>
```
A Video will usually have 5 or more entities for each upload, so a Curator will need to check which entities are associated with the Video, and delete them "backwards". If you want to remove the Video with `entityId` 200...
```
$ joystream-cli content-directory:entity 200
$ joystream-cli content-directory:removeEntity 200

$ joystream-cli content-directory:entity 199
$ joystream-cli content-directory:removeEntity 199

$ joystream-cli content-directory:entity 198
$ joystream-cli content-directory:removeEntity 198

$ joystream-cli content-directory:entity 197
$ joystream-cli content-directory:removeEntity 197

$ joystream-cli content-directory:entity 196
$ joystream-cli content-directory:removeEntity 196

$ joystream-cli content-directory:entity 195
# When you a see a new Video or Channel entity (or something else unrelated), you are clear and must stop
```
