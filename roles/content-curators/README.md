<p align="center"><img src="img/content-curators.svg"></p>

<div align="center">
  <h4>This is a guide for applying, and working as a Content Curator on the latest
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
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
  - [Content](#content)
  - [Channels](#channels)
    - [Discretion](#discretion)
- [Advanced](#advanced)
  - [Channel](#channel)
      - [Verify](#verify)
      - [Remove Verification](#remove-verification)
      - [Censor](#censor)
      - [Un-Censor](#un-censor)
  - [Content](#content-1)
      - [Content License and Attribution](#content-license-and-attribution)
      - [Curation Status](#curation-status)
<!-- TOC END -->

# Overview

This page will contain all information on how to apply for the role of `Content Curator`, and how to perform the various tasks required for the job.

# Hiring Process

First, open [Pioneer](testnet.joystream.org/), and navigate to the `Working groups` sidebar. Here you will find an overview of the current `Content Curators`, and the `Content Lead`. In the `Opportunities` tab, you can get an overview of future, current and previous openings, along with terms, settings, status and history (if applicable). The terms and settings include the following parameters to consider:

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
- If you attempt to apply with insufficient stake.
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

The main job for curators is to regularly check the content directory and channels, and checking that rules and guidelines are being followed. The basic rules are stated below.

## Content

Curators are responsible for ensuring the following:
1. Content are not in violation with the platform [ToS](https://testnet.joystream.org/#/pages/tos), meaning
  - illicit should be `censored`, and marked for takedown
  - content must be given assigned the appropriate license and, if required, attribution
  - explicit content must be marked as such
2. Content is resolving and playing as intended
  - content that is not playable should be marked as unlisted, and a heads up should be given to the channel owner in the forum
3. Metadata is correct
  - incorrect metadata should be corrected, unless the mistake requires more severe consequences (see 1.)

In order to achieve this, they need to get familiarized with the Joystream Versioned Store system, outlined [here](https://github.com/Joystream/joystream-content-system)

## Channels
Channels should be treated the same way as content, and the following basic rules should be enforced:
- Channels that consistently violate the rules for [content](#content), should be censored or closed
- Channels that delivers standout content should get "verified" on the platform

### Discretion

These rules are not clearly defined in all cases, so it's important that curators are able to use discretion. In many cases, it's preferable to try and get in touch with the channel owner first, rather than immediately pull the trigger. If in doubt, contact the `Lead` first. In other cases, immediate action may be required.

"Speak softly, and carry a big stick"
- Theodore Roosevelt

# Advanced

Some of the tasks expected by curators require manual [extrinsics](https://testnet.joystream.org/#/extrinsics). Not  all required tasks can be done in the UI directly, but they can all be done through extrinsics.

Some operations require you to add the `curatorId` you wish to make the extrinsic with as input. This can be found with a [chain state](https://testnet.joystream.org/#/chainstate) query:
- Select `contentWorkingGroup`, then `curatorById` with the dropdowns, then see which ID matches your account. This should be an integer > 0.


## Channel

The table below outlines which operations can be done, and how to update them:

| Action                  | Source     | Instructions                                     |
|-------------------------|------------|--------------------------------------------------|
| `Verify`                | UI         |[Link](#verify)                                   |
| `Remove Verification`   | UI         |[Link](#remove-verification)                      |
| `Censor`                | UI         |[Link](#censor)                                   |
| `Un-Censor`             | UI         |[Link](#un-censor)                                |

#### Verify

If you are a `Content Curator`, with the role key loaded in Pioneer, you will automatically have the option to perform this task. If the channel you wish to perform the action on is visible under the [Media](https://testnet.joystream.org/#/media) sidebar, it will appear next to it.

If you want to perform the action on a specific channel, navigate to it, and you will see the option in your browser. Channels can be accessed directly with the URL `https://testnet.joystream.org/#/media/channels/<n>`, where `<n>` is an integer.
E.g. - `https://testnet.joystream.org/#/media/channels/1` for the "Staked" channel.

The same options will be appear if you navigate to a content `entity`, added under the channel.

The UI will automatically select the appropriate key and credential, and preview the action you want to make.

#### Remove Verification

Same as [this](#verify).

#### Censor

Same as [this](#verify).

#### Un-Censor

Same as [this](#verify).

## Content
For content, all the actions performed includes changing one or more parameters in the `Versioned Store`. This requires more knowledge about how the system works.
The table below outlines the key actions that can be performed, with links to rough instructions:

| Action                  | Source     | Type      | Instructions                                     |
|-------------------------|------------|-----------|--------------------------------------------------|
| `Content License`       | Extrinsic  |`Internal` | [Link](#content-license-and-attribution)         |
| `Attribution`           | Extrinsic  |`Text`     | [Link](#content-license-and-attribution)         |
| `Curation Status`       | Extrinsic  |`Internal` | [Link](#curation-status)                         |

#### Content License and Attribution

The Content License and its related property Attribution are both important to have configured correctly. Content that should be set as "Creative Commons" which would be in line with the Terms of Service if marked as such combined the appropriate attribution, would instead be violating these terms if another license, or missing/incorrect attribution is set.

In order to change this, access a piece of content in the UI. The URL will end with a number, namely the `entityId` in the content directory.

Suppose you have an entity `n`, that incorrectly is tagged with the "Public Domain" license, and has no attribution set, whereas it should have been tagged with the "Creative Commons" license, and include an attribution to the original creator.

##### Get the necessary information

By doing a [chain state](https://testnet.joystream.org/#/chainstate) query, one can get find the required information to edit this:

- First select `versionedStore`, then `entityById` with the dropdowns, then type in the `entityId`, and click the plus button. This will return a json with the current state of this Entity.
- The second entry in the json will be `"class_id":n`, where `n` is the Class the Entity belongs to. eg. `7` for the "Video" Class.
- Change the second dropdown to `classById`, or find the class in the [Content System repo](https://github.com/Joystream/joystream-content-system/) for ease of use.
- Find the `in_class_index`, corresponding to the name of the "License" and "Attribution", along with the "type" of each.
- For an Entity in the Video Class, with `schemaId` = 0:
  - "License": `in_class_index` is 11, "type" is `Internal` (where `classId` is 3 - "Content License").
  - "Attribution": `in_class_index` is 12, "type" is `Text`.
- This means you have to use the `classId`, and find the Entities in that Class.
- The Content License Class has `classId` = 3
- With `schemaId` = 0, the Entities can be found [here](https://github.com/Joystream/joystream-content-system/blob/master/entities/general/content-license.md)

Further, you need to know the `curatorId` you wish to make the extrinsic with. This can be found by:
- Select `contentWorkingGroup`, then `curatorById` with the dropdowns, then see which ID matches your account. This should be an integer > 0.

##### Making the extrinsic

When changing an entity as a curator, it's good practice to simultaneously change the [Curation Status](#curation-status). This can and should be done in the same transaction, but can also be done consequently. In the example below, it's excluded, but it should be easy enough to perform if you read the section in the link before you make the transaction.

Go to [extrinsics](https://testnet.joystream.org/#/extrinsics), and input the following:
- Select the correct account you wish the perform the extrinsic with (namely, your curator role account)
- Select `versionedStorePermissions` and `updateEntityPropertyValues` in the first two dropdowns
- Set `with_credential` to 1 (as curator)
- Keep `as_entity_maintainer` as No/False
- Set `entity_id` to `n`
- In our example:
  - Click the `+ Add item` button, and set the `in_class_index` to 11, and `value` to `Internal` for Content License
  - In the new field `Internal`, type in 193 for "Creative Commons (attribution required)".
  - Click the `+ Add item` button, and set the `in_class_index` to 12, and `value` to `Text` for Attribution
  - In the new field `Text`, type in an appropriate attribution to the original creator.
**Note: Make sure you have a terminal open with a node log running with the flag `--log runtime`. This will provide a source of error, should you have made incorrect input**
- Click the `Submit Transaction` button, verify your input, type in the password and confirm.
- If you used the correct input, the transaction will modify the `entity`.



#### Curation Status

The Curation Status covers allows curators to censor or modify an entity, while also providing a rationale for doing so. It should always be included while performing a modification, and is the first line that should be taken for content in violation of the Terms of Service.

##### Get the necessary information

By doing a [chain state](https://testnet.joystream.org/#/chainstate) query, one can get find the required information to edit this:

- First select `versionedStore`, then `entityById` with the dropdowns, then type in the `entityId`, and click the plus button. This will return a json with the current state of this entity.
- The second entry in the json will be `"class_id":n`, where `n` is the Class the Entity belongs to, eg. `7` for the "Video" Class.
- Change the second dropdown to `classById`, or find the class in the [Content System repo](https://github.com/Joystream/joystream-content-system/) for ease of use.
- Find the `in_class_index`, corresponding to the name of the "Curation Status", along with its "type".
- For an Entity in the Video Class, with `schemaId` = 0:
  - "Curation Status": `in_class_index` is 9, "type" is `Internal` (where `classId` is 5 - "Curation Status").
- This means you have to use the `classId`, and find the Entities in that Class.
- With `schemaId` = 0, the Entities can be found [here](https://github.com/Joystream/joystream-content-system/blob/master/entities/general/curation-status.md)


##### Making the extrinsic

Go to [extrinsics](https://testnet.joystream.org/#/extrinsics), and input the following:
- Select the correct account you wish the perform the extrinsic with (namely, your curator role account)
- Select `versionedStorePermissions` and `updateEntityPropertyValues` in the first two dropdowns
- Set `with_credential` to 1 (as curator)
- Keep `as_entity_maintainer` as No/False
- Set `entity_id` to `n`
- In our example:
  - Click the `+ Add item` button, and set the `in_class_index` to 9, and `value` to `Internal` for Curation Status
  - In the new field `Internal`, type in 187 for "Edited".
**Note: Make sure you have a terminal open with a node log running with the flag `--log runtime`. This will provide a source of error, should you have made incorrect input**
- Click the `Submit Transaction` button, verify your input, type in the password and confirm.
- If you used the correct input, the transaction will modify the `entity`.
