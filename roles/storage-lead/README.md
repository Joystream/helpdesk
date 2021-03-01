<p align="center"><img src="img/storage-lead.svg"></p>

<div align="center">
  <h4>This is a guide to working as the Storage Provider Lead on the latest
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
</div>



Table of Contents
==
<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
- [Overview](#overview)
- [About The Storage Lead](#about-the-storage-lead)
- [Hiring Storage Lead](#hiring-storage-lead)
  - [Proposals](#proposals)
    - [Create Opening](#create-opening)
    - [Review Applications](#review-applications)
    - [Processing Applications](#processing-applications)
- [Hiring Storage Providers](#hiring-storage-providers)
  - [Using the CLI](#using-the-cli)
    - [Create Opening](#create-opening-1)
    - [Accepting Applications](#accepting-applications)
    - [Processing Applications](#processing-applications-1)
- [Working As Storage Lead](#working-as-storage-lead)
  - [Responsibilities](#responsibilities)
  - [All Commands](#all-commands)
<!-- TOC END -->


# Overview

This page contains all the information required on becoming `Storage Provider Lead`, and how to perform the various tasks required for the job.

# About The Storage Lead

The `Storage Working Group Lead`, `Storage Provider Lead` or simply `Storage Lead` is a new role introduced as part of the _Nicaea_ upgrade to our Constantinople testnet. The `Storage Lead` is hired directly by the council through the proposals system and is responsible for the hiring, firing and wider management of `Storage Providers` on the network.

# Hiring Storage Lead

## Proposals

Hiring the `Storage Lead` is the responsibility of the `Council` through the proposals system. Three new proposal types have been introduced to support the hiring process, and more have also been added to allow the `Council` to effectively manage the lead once "in office", through slashing, setting the mint capacity, decreasing stake and firing etc.

### Create Opening

The first step from the Council's perspective is creating an opening where prospective `Storage Leads` can apply for the role.
Within [Pioneer](https://testnet.joystream.org), navigate first to the proposals tab and select `New Proposal`.

To create an opening, select `Add Working Group Leader Opening` and fill in the variables.

### Review Applications

In order to formally "close" the opening to further applicants and inform the existing candidates that their submissions are currently being considered, the status of the opening must be changed to "In Review".

This can be done very easily through the creation of another proposal by the `Council`, this time with the `Begin Review Working Group Leader Application` proposal type. The main thing to pay attention to here is the `Working Group Opening ID` created earlier. Helpfully there is a dropdown box for choosing among the currently active openings, in case you have forgotten the ID.

### Processing Applications

The final step in hiring the `Storage Lead` is to create a `Fill Working Group Leader Opening`. The requirements here simply to choose the relevant opening from the drop-down menu and choose between the candidate applications (in JSON format) shown on the page.

Once a candidate has been chosen, and the final proposal has passed, the focus is now on the new `Storage Lead`...

# Hiring Storage Providers

## Using the CLI
Our newly developed Command-Line Interface (CLI) is an essential tool for the Storage Lead, as it is by far the simplest way to hire and manage `Storage Providers` and applicants for this role. The program and its instructions for use can be found [here](https://github.com/Joystream/joystream/tree/master/cli).

All the useful commands which can be executed by the `Storage Lead` will require the lead to import their "role" key rather than their "member" key. Consequently, in the CLI the `account:import` and `account:choose` commands will need to be used.

### Create Opening

To create an opening, the lead needs to run the `working-groups:createOpening` command using their role key.

There are some options for specific purposes which can be selected with this command, as shown below:
```
Create working group opening (requires lead access)

USAGE
  $ joystream-cli working-groups:createOpening

OPTIONS
  -e, --edit                               If provided along with --input - launches in edit mode allowing to modify the input before sending the exstinsic

  -g, --group=(storageProviders|curators)  The working group context in which the command should be executed
                                           Available values are: storageProviders, curators.

  -i, --input=input                        Path to JSON file to use as input (if not specified - the input can be provided interactively)

  -o, --output=output                      Path to the file where the output JSON should be saved (this output can be then reused as input)

  --dryRun                                 If provided along with --output - skips sending the actual extrinsic(can be used to generate a "draft" which can be provided as input
                                           later)
```

Note that although some values are stated as `u128` or other confusing types, you should provide a plaintext or numbers, and the CLI will convert them for you. Once this command is run, the prompts to set up the opening are *somewhat* self-explanatory.
However, here are some pointers when creating an Opening.

#### Application Parameters
- `Choose value for activate_at:`
  - Use `CurrentBlock` for allowing applications right away
- `Do you want to provide the optional application_rationing_policy parameter?`
  - This lets you set a max number of active applicants (`n`).
  - Can be useful to avoid "spam", and combined with
  - This lets you require an application stake from the Applicants
  - Combined with setting `role/application_staking_policy`, and `at_least` for one or both, only the `n` applicants with the highest combined `role+application` stake will be considered.
- `Provide value for max_review_period_length` should be high enough to allow you enough time to review. If the Review Period expires, the Opening closes, and no one is hired.
- The various `*_unstaking_period_length` parameters means all take an argument `x` in blocks
  - `crowded_out_unstaking_period_length` - "Application" and/or "Role" stake:
    - If an applicant is crowded out due to the `number_of_applicants>n`, this lets you set an "unstaking period". May not make much sense, as they may want to re-apply with (a) higher stakes, and this will block them from re-using said stake(s) for `x` blocks.
  - `review_period_expired_unstaking_period_length` - "Application" and/or "Role" stake:
    - If the Opening expired with no one hired, this keeps their stake(s) locked for `x` blocks. May be overly harsh?
  - `fill_opening_successful_applicant_application_stake_unstaking_period` - Only "Application" stake:
    - If an Opening is ended with one or more Workers hired, `x`is the number of blocks until the hired Worker(s) Application stake is returned.
  - `fill_opening_failed_applicant_*_stake_unstaking_period` - "Application" and/or "Role" stake:
    - If an Opening is ended with one or more Workers hired, `x`is the number of blocks until the Application stake is returned to those that were not hired.
  - `terminate_*_stake_unstaking_period` - "Application" and/or "Role" stake:
    - If an Application was terminated, this keeps their stake(s) locked for `x` blocks. May be useful to stop spammers.
    - If no one was hired, this keeps their Application stake locked for `x` blocks. May be overly harsh?
  - `exit_role_*_stake_unstaking_period` - "Application" and/or "Role" stake:
    - If a Worker exits their role, this keeps their stake(s) locked for `x` blocks.
    - Should be used for the Role stake
    - Maybe not so useful for the Application stake?

#### Human Readable Information and Questions
The second part is filling out a JSON schema, where you can set what information is provided to applicants and what details are collected as part of the application process. As mentioned above, you should consider creating a draft first, to review your input before broadcasting on-chain. Here are some pointers:
- When prompted for a version, provide the value `1`.
- When providing "type" for the `questions vector`, `text` means single line, whereas `text area` means a multi-line text area.

#### Complete Example
```
? Your account's password [hidden]
  Choose value for activate_at: CurrentBlock
  Providing values for commitment struct:
    Do you want to provide the optional application_rationing_policy parameter? Yes
      Providing values for {
        max_active_applicants:u32
      } struct:
        Provide value for max_active_applicants 3
    Provide value for max_review_period_length 14400
    Do you want to provide the optional application_staking_policy parameter? Yes
      Providing values for {
        amount:u128
        amount_mode:{"_enum":["AtLeast","Exact"]}
        crowded_out_unstaking_period_length:Option<u32>
        review_period_expired_unstaking_period_length:Option<u32>
      } struct:
        Provide value for amount 1000
        Choose value for amount_mode: AtLeast
        Do you want to provide the optional crowded_out_unstaking_period_length parameter? Yes
          Provide value for u32 1
        Do you want to provide the optional review_period_expired_unstaking_period_length parameter? Yes
          Provide value for u32 2
    Do you want to provide the optional role_staking_policy parameter? Yes
      Providing values for {
        amount:u128
        amount_mode:{"_enum":["AtLeast","Exact"]}
        crowded_out_unstaking_period_length:Option<u32>
        review_period_expired_unstaking_period_length:Option<u32>
      } struct:
        Provide value for amount 1001
        Choose value for amount_mode: AtLeast
        Do you want to provide the optional crowded_out_unstaking_period_length parameter? Yes
          Provide value for u32 3
        Do you want to provide the optional review_period_expired_unstaking_period_length parameter? Yes
          Provide value for u32 4
    Do you want to provide the optional fill_opening_successful_applicant_application_stake_unstaking_period parameter? Yes
      Provide value for u32 5
    Do you want to provide the optional fill_opening_failed_applicant_application_stake_unstaking_period parameter? Yes
      Provide value for u32 6
    Do you want to provide the optional fill_opening_failed_applicant_role_stake_unstaking_period parameter? Yes
      Provide value for u32 7
    Do you want to provide the optional terminate_application_stake_unstaking_period parameter? Yes
      Provide value for u32 8
    Do you want to provide the optional terminate_role_stake_unstaking_period parameter? Yes
      Provide value for u32 9
    Do you want to provide the optional exit_role_application_stake_unstaking_period parameter? Yes
      Provide value for u32 10
    Do you want to provide the optional exit_role_stake_unstaking_period parameter? Yes
      Provide value for u32 11
Providing values for human_readable_text struct:
    Provide value for version 1
    Provide value for headline Some Headline
    Providing values for job struct:
      Provide value for title Some Title
      Provide value for description Some Description
    Providing values for application struct:
      Providing values for sections vector:
        Do you want to add another entry to sections vector (currently: 0)? Yes
        Providing values for {
          title:Text
          questions:Vec<{"title":"Text","type":"Text"}>
        } struct:
          Provide value for title Sections Title 0
          Providing values for questions vector:
            Do you want to add another entry to questions vector (currently: 0)? Yes
            Providing values for {
              title:Text
              type:Text
            } struct:
              Provide value for title Questions Title 0
              Provide value for type text area
            Do you want to add another entry to questions vector (currently: 1)? Yes
            Providing values for {
              title:Text
              type:Text
            } struct:
              Provide value for title Questions Title 1
              Provide value for type text
            Do you want to add another entry to questions vector (currently: 2)? Yes
            Providing values for {
              title:Text
              type:Text
            } struct:
              Provide value for title Questions Title 2
              Provide value for type text area
            Do you want to add another entry to questions vector (currently: 3)? No
        Do you want to add another entry to sections vector (currently: 1)? Yes
        Providing values for {
          title:Text
          questions:Vec<{"title":"Text","type":"Text"}>
        } struct:
          Provide value for title Sections Title 1
          Providing values for questions vector:
            Do you want to add another entry to questions vector (currently: 0)? Yes
            Providing values for {
              title:Text
              type:Text
            } struct:
              Provide value for title Questions Title 0 in Section 1
              Provide value for type text
            Do you want to add another entry to questions vector (currently: 1)? No
        Do you want to add another entry to sections vector (currently: 2)? No
    Provide value for reward x tJOY per n blocks
    Providing values for creator struct:
      Providing values for membership struct:
        Provide value for handle Lead
    Providing values for process struct:
      Providing values for details vector:
        Do you want to add another entry to details vector (currently: 0)? Yes
        Provide value for Text Detail 0
        Do you want to add another entry to details vector (currently: 1)? Yes
        Provide value for Text Detail 1
        Do you want to add another entry to details vector (currently: 2)? No
```
If successfully submitted, you can look at your Opening using the `working-groups:opening <WGOPENINGID>`, which returns:
```
Group: storageProviders

______________ Human readable text _______________

{
    version: 1,
    headline: "Some Headline",
    job: {
        title: "Some Title",
        description: "Some Description"
    },
    application: {
        sections: [
            {
                title: "Sections Title 0",
                questions: [
                    {
                        title: "Questions Title 0",
                        type: "text area"
                    },
                    {
                        title: "Questions Title 1",
                        type: "text"
                    },
                    {
                        title: "Questions Title 2",
                        type: "text area"
                    }
                ]
            },
            {
                title: "Sections Title 1",
                questions: [
                    {
                        title: "Questions Title 0 in Section 1",
                        type: "text"
                    }
                ]
            }
        ]
    },
    reward: "x tJOY per n blocks",
    creator: {
        membership: {
            handle: "Lead"
        }
    },
    process: {
        details: [
            "Detail 0",
            "Detail 1"
        ]
    }
}

________________ Opening details _________________

WG Opening ID                 8                                
Opening ID                    10                               
Type                          Worker                           
Stage                         Accepting Applications           
Last status change            ~ 6:31:06 AM 7/29/2020 (#194118)
Application stake             >= 1.000k JOY                    
Role stake                    >= 1.001k JOY                    

_______________ Unstaking periods ________________

Crowded Out Application Stake Unstaking Period Length:                  1 blocks  
Crowded Out Role Stake Unstaking Period Length:                         3 blocks  
Exit Role Application Stake Unstaking Period:                           10 blocks
Exit Role Stake Unstaking Period:                                       11 blocks
Fill Opening Failed Applicant Application Stake Unstaking Period:       6 blocks  
Fill Opening Failed Applicant Role Stake Unstaking Period:              7 blocks  
Fill Opening Successful Applicant Application Stake Unstaking Period:   5 blocks  
Review Period Expired Application Stake Unstaking Period Length:        2 blocks  
Review Period Expired Role Stake Unstaking Period Length:               4 blocks  
Terminate Application Stake Unstaking Period:                           8 blocks  
Terminate Role Stake Unstaking Period:                                  9 blocks  
```


### Accepting Applications

Once enough applications have been submitted, these can now be reviewed to decide who should be hired as a `Storage Provider`.
The command to be used is the following: `working-groups:startReviewPeriod <WGOPENINGID>`.

You can find the `WGOPENINGID` in the URL in Pioneer or through a chain state query of the currently active openings.

### Processing Applications

As soon as the opening is in the `In Review` state, you can start hiring!

Simply run `working-groups:fillOpening <WGOPENINGID>` where `<WGOPENINGID>` is the same as earlier, and you will be prompted to select the applicants you wish to hire (using a check-box dialog). The usernames of the candidates will be shown, so you don't have to worry about numerical IDs for this part.

# Working As Storage Lead

## Responsibilities
As the `Storage Lead` you are responsible for ensuring that `Storage Providers` are performing adequately. They must hold a complete and up-to-date copy of the content directory and ensure the uptime in order to effectively serve testnet content consumers.

If a `Storage Provider` is not performing adequately it is up to you to decide the sanctions for this, which may include slashing and, as a last resort, their eviction from the Storage Working Group.

## All Commands

Within the CLI, all the relevant commands for the Storage Lead can be found through the following query:
```
working-groups --help
```
More information on the usage can be found [here](/tools/cli)

For convenience, the output of this command is listed below to give a sense of the powers and responsibilities of the Storage Lead:
```
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
