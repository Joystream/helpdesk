<p align="center"><img src="img/content-curator-lead.svg"></p>

<div align="center">
  <h4>This is a guide to working as the Content Curator Lead on the latest
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
</div>



Table of Contents
==
<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
- [Table of Contents](#table-of-contents)
- [Overview](#overview)
- [About The Curator Lead](#about-the-curator-lead)
- [Hiring Curator Lead](#hiring-curator-lead)
  - [Proposals](#proposals)
    - [Create Opening](#create-opening)
    - [Review Applications](#review-applications)
    - [Processing Applications](#processing-applications)
- [Hiring Content Curators](#hiring-content-curators)
  - [Using the CLI](#using-the-cli)
    - [Create Opening](#create-opening-1)
    - [Accepting Applications](#accepting-applications)
    - [Processing Applications](#processing-applications-1)
- [Working As Content Curator Lead](#working-as-content-curator-lead)
  - [Responsibilities](#responsibilities)
    - [Curation](#curation)
    - [Firing Curators](#firing-curators)
    - [Content Working Group Mint](#content-working-group-mint)
      - [Replenishing The Mint](#replenishing-the-mint)
- [Troubleshooting](#troubleshooting)
<!-- TOC END -->

# Overview

This page will contain all information on how to become `Content Curator Lead`, and how to perform the various tasks required for the job.

# About The Curator Lead

Since the introduction of the proposals system for the Constantinople testnet, the `Council` has had the power to appoint a `Content Curator Lead` for the network.

# Hiring Curator Lead

## Proposals

Hiring the `Curator Lead` is the responsibility of the `Council` through the proposals system. Three new proposal types have been introduced to support the hiring process, and more have also been added to allow the `Council` to effectively manage the lead once "in office", through slashing, setting the mint capacity, decreasing stake and firing etc.

### Create Opening

The first step from the Council's perspective is creating an opening where prospective `Curator Leads` can apply for the role.
Within [Pioneer](https://testnet.joystream.org), navigate first to the proposals tab and select `New Proposal`.

To create an opening, select `Add Working Group Leader Opening` and fill in the variables.

### Review Applications

In order to formally "close" the opening to further applicants and inform the existing candidates that their submissions are currently being considered, the status of the opening must be changed to "In Review".

This can be done very easily through the creation of another proposal by the `Council`, this time with the `Begin Review Working Group Leader Application` proposal type. The main thing to pay attention to here is the `Working Group Opening ID` created earlier. Helpfully there is a dropdown box for choosing among the currently active openings, in case you have forgotten the ID.

### Processing Applications

The final step in hiring the `Curator Lead` is to create a `Fill Working Group Leader Opening`. The requirements here are simply to choose the relevant opening from the drop-down menu and choose betwen the candidate applications (in JSON format) shown on the page.

Once a candidate has been chosen and the final proposal has passed, the focus is now on the new `Curator Lead`...

# Hiring Content Curators

As the person responsible for the platforms content curation, the Lead may find additional manpower is required, and can hire `Content Curators` to assist.

## Using the CLI
Our newly developed Command-Line Interface (CLI) is an essential tool for the Curator Lead, as it is by far the simplest way to hire and manage `Curator Providers` and applicants for this role. The program and its instructions for use can be found [here](https://github.com/Joystream/joystream/tree/master/cli).

All of the useful commands which can be executed by the `Curator Lead` will require the lead to import their "role" key rather than their "member" key. Consequently, in the CLI the `account:import` and `account:choose` commands will need to be used.

All the commands available for managing the workers are available by using the command `joystream-cli working-groups --help`, which returns:
```
Working group lead and worker actions

USAGE
  $ joystream-cli working-groups:COMMAND

COMMANDS
  working-groups:application                 Shows an overview of given application by Working Group Application ID
  working-groups:createOpening               Create working group opening (requires lead access)
  working-groups:decreaseWorkerStake         Decreases given worker stake by an amount that will be returned to the worker role account. Requires lead access.
  working-groups:evictWorker                 Evicts given worker. Requires lead access.
  working-groups:fillOpening                 Allows filling working group opening that's currently in review. Requires lead access.
  working-groups:increaseStake               Increases current role (lead/worker) stake. Requires active role account to be selected.
  working-groups:leaveRole                   Leave the worker or lead role associated with currently selected account.
  working-groups:opening                     Shows an overview of given working group opening by Working Group Opening ID
  working-groups:openings                    Shows an overview of given working group openings
  working-groups:overview                    Shows an overview of given working group (current lead and workers)
  working-groups:setDefaultGroup             Change the default group context for working-groups commands.
  working-groups:slashWorker                 Slashes given worker stake. Requires lead access.
  working-groups:startAcceptingApplications  Changes the status of pending opening to "Accepting applications". Requires lead access.
  working-groups:startReviewPeriod           Changes the status of active opening to "In review". Requires lead access.
  working-groups:terminateApplication        Terminates given working group application. Requires lead access.
  working-groups:updateRewardAccount         Updates the worker/lead reward account (requires current role account to be selected)
  working-groups:updateRoleAccount           Updates the worker/lead role account. Requires member controller account to be selected
  working-groups:updateWorkerReward          Change given worker's reward (amount only). Requires lead access.
  ```

### Create Opening

To create an opening, the lead needs to run the `working-groups:createOpening -g curators` command using their role key.

There are some options for specific purposes which can be selected with this command, as shown below:
```
Create working group opening (requires lead access)

USAGE
  $ joystream-cli working-groups:createOpening

OPTIONS
  -e, --edit                               If provided along with --input - launches in edit mode allowing to modify the input before sending the exstinsic

  -g, --group=(CuratorProviders|curators)  The working group context in which the command should be executed
                                           Available values are: CuratorProviders, curators.

  -i, --input=input                        Path to JSON file to use as input (if not specified - the input can be provided interactively)

  -o, --output=output                      Path to the file where the output JSON should be saved (this output can be then reused as input)

  --dryRun                                 If provided along with --output - skips sending the actual extrinsic(can be used to generate a "draft" which can be provided as input
                                           later)
```

Note that although some values are stated as `u128` or other confusing types, you should provide plaintext or numbers, and the CLI will convert them for you. Once this command is run, the prompts to set up the opening are *somewhat* self-explanatory. Feel free to ask, or give it a try with a --dryRun first :)


If successfully submitted, you can look at your Opening using the `working-groups:opening <WGOPENINGID> -g curators`, which returns something like:

```
Current Group: curators

______________ Human readable text _______________

{
    version: 1,
    headline: "Curator application",
    job: {
        title: "Curators",
        description: "You can become a curator!"
    },
    application: {
        sections: null
    },
    reward: "10 tJOY per 600 blocks",
    creator: {
        membership: {
            handle: "yourHandle"
        }
    },
    process: {
        details: [

        ]
    }
}

________________ Opening details _________________

WG Opening ID                 1                                   
Opening ID                    22                                  
Type                          Worker                              
Stage                         Complete                            
Last status change            ~ 10:12:54 AM 12/10/2020 (#1251432)
Application stake             == 500.000 JOY                      
Role stake                    == 500.000 JOY                      

_______________ Unstaking periods ________________

Crowded Out Application Stake Unstaking Period Length:                  0 blocks
Crowded Out Role Stake Unstaking Period Length:                         0 blocks
Exit Role Application Stake Unstaking Period:                           0 blocks
Exit Role Stake Unstaking Period:                                       0 blocks
Fill Opening Failed Applicant Application Stake Unstaking Period:       0 blocks
Fill Opening Failed Applicant Role Stake Unstaking Period:              0 blocks
Fill Opening Successful Applicant Application Stake Unstaking Period:   0 blocks
Review Period Expired Application Stake Unstaking Period Length:        0 blocks
Review Period Expired Role Stake Unstaking Period Length:               0 blocks
Terminate Application Stake Unstaking Period:                           0 blocks
Terminate Role Stake Unstaking Period:                                  0 blocks

________________ Applications (0) ________________        
```

### Accepting Applications

Once enough applications have been submitted, these can now be reviewed to decide who should be hired as a `Content Curator`.
The command to be used is the following: `working-groups:startReviewPeriod <WGOPENINGID> -g curators`.

You can find the `WGOPENINGID` in the URL in Pioneer or using the CLI command `working-groups:openings -g curators`

### Processing Applications

As soon as the opening is in the `In Review` state, you can start hiring!

Simply run `working-groups:fillOpening <WGOPENINGID> -g curators` where `<WGOPENINGID>` is the same as earlier, and you will be prompted to select the applicants you wish to hire (using a check-box dialog). The usernames of the candidates will be shown so you don't have to worry about numerical IDs for this part.

# Working As Content Curator Lead

## Responsibilities

Other than the hiring aspect of the role as `Content Curator Lead`, the lead should try to coordinate the actions of the other curators and decide on priorities for curation.

If necessary, upon discussing with the council, the `Content Curator Lead` can also decide to fire curators who are not performing their jobs adequately.

Most of the time however, the responsibilities of the `Content Curator Lead` will be very similar to those of a standard `Content Curator`. You can read about these responsibilities in [this section](../roles/content-curators#content) of the guide for `Content Curators`.

### Curation
The main task of the `Curators` is curating the content on chain.

The easiest way is to simply "hide" content by using the `curateContent` command. However, the Curator Lead must first enable curation:
```
# Create a new group:
$ joystream-cli content-directory:createCuratorGroup

# Add curator to the group:
$ joystream-cli content-directory:addCuratorToGroup <GROUPID> <CURATORID>

# Give the group class privileges, (it's most useful to add classes "Channel" and "Video"):
$ joystream-cli content-directory:addMaintainerToClass <CLASSNAME> <GROUPID>

# Make the group active:
$ joystream-cli content-directory:setCuratorGroupStatus <GROUPID>

# Overview of the group(s)
$ joystream-cli content-directory:curatorGroups
```

By creating more groups, the Lead can choose which `Curators` you want to give maintainer status across the individual classes. The Lead should include themselves access to each class.

### Firing Curators
Unfortunately, it may sometimes be necessary to fire curators who are not doing their jobs correctly.

Use the command `joystream-cli working-groups:evictWorker <WORKERID> -g curators` and follow the instructions.

### Content Working Group Mint
To check the details of the current Content Working Group Mint:

(1) Use the following chain state query to determine the current mint ID: `contentDirectoryWorkingGroup -> mint`.<br>
(2) Check the details of the mint using the following query: `minting -> mints`.

#### Replenishing The Mint
It will sometimes be necessary to replenish the Content Working Group Mint. This can be done through a `Set Working Group Mint Capacity` proposal [here](https://testnet.joystream.org/#/proposals/new) which must be approved by the Council in order to take effect. For this reason it is best to discuss these sorts of proposals with the Council before making them.

---

# Troubleshooting
If you need help with some of the more advanced operations associated with being the `Content Curator Lead` (e.g. maintaining the versioned store), please simply ask for help in the [Telegram group](https://t.me/JoyStreamOfficial) or get in touch with one of the Jsgenesis team directly.
