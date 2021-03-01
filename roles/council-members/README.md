<p align="center"><img src="img/council-members_new.svg"></p>

<div align="center">
  <h4>This is a step-by-step guide on the Joystream Council, allowing users to take part in the governance system for the
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
</div>

Overview
===
This page contains a detailed guide about how the governance system works on the current Joystream testnet, and how you can participate. This page is intended primarily for those wanting to become, or who already are Council Members ("CMs").

Nonetheless, if you are interested in the Joystream project more generally and/or want to become a part of the community now or in the future, there is lots of information in here that will help you understand the project and the governance of the platform at a higher level.

Table of Contents
---
<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
- [Why Become a Council Member](#why-become-a-council-member)
  - [Rewards and Incentives](#rewards-and-incentives)
    - [Recurring Rewards](#recurring-rewards)
    - [KPI Rewards](#kpi-rewards)
      - [Example](#example)
  - [Get Started](#get-started)
- [Council Elections](#council-elections)
  - [Parameters](#parameters)
  - [Council Election Cycle](#council-election-cycle)
    - [Announcing](#announcing)
      - [How to Announce](#how-to-announce)
      - [End of Announcing](#end-of-announcing)
    - [Voting](#voting)
      - [How to Vote](#how-to-vote)
    - [Revealing](#revealing)
      - [How to Reveal](#how-to-reveal)
      - [End of Revealing](#end-of-revealing)
    - [Term](#term)
- [How to Get Elected](#how-to-get-elected)
  - [Announce on the Forum](#announce-on-the-forum)
- [Elected Council Members](#elected-council-members)
  - [Tasks Overview](#tasks-overview)
  - [Council KPIs](#council-kpis)
    - [Scope of Work](#scope-of-work)
      - [Council Deliverables](#council-deliverables)
      - [Chain Values](#chain-values)
    - [Reports](#reports)
    - [Council Secretary](#council-secretary)
    - [Managing the Working Groups](#managing-the-working-groups)
      - [Cost Control](#cost-control)
      - [General Performance](#general-performance)
      - [Council Actions](#council-actions)
    - [Managing Community Bounties](#managing-community-bounties)
      - [Reward Distribution](#reward-distribution)
      - [Format](#format)
      - [Workflow](#workflow)
      - [Steps](#steps)
      - [Councils Role](#councils-role)
- [Governance](#governance)
  - [Proposals](#proposals)
  - [Voting on Proposals](#voting-on-proposals)
<!-- TOC END -->



# Why Become a Council Member
As the governance system is arguably the most important component of the platform on mainnet, we are relying on testnets to train and build up an experienced and highly competent group of initial community members that can diligently perform the tasks required of them once we reach the mainnet stage.

A "good" Council needs CMs that all have a strong understanding of both the platform's token economics (["tokenomics"](/tokenomics)) and each of the individual Working Groups, and the roles each of these play in making the platform function. Additionally, the composition of each Council should ensure that the group has expertise in every domain, and some CMs with low-level technical understanding will likely be required to provide guidance on other aspects of the project (marketing, legal, strategy etc.).

## Rewards and Incentives
During the Constantinople testnet, Jsgenesis realized we need to put a lot more effort in to attracting, training and retaining these high-quality people. CMs will now be a generously paid role on the platform, and in the new KPI scheme, also see direct rewards for those Councils doing a good job.

Consequently, Jsgenesis will take an active role in the elections. More information on how to apply, and increase your chances of getting elected can be found [here](#council-election-cycle).

### Recurring Rewards
A newly elected Council will automatically be assigned a recurring reward that automatically pays out tokens every `n`th block. The magnitude of this reward may change over time, but can be monitored on the [Tokenomics page](https://testnet.joystream.org/#/tokenomics).

### KPI Rewards
The KPI rewards will depend on the Council's performance. Jsgenesis will provide a new set of [Council KPIs](#council-kpis) for each new term, with some variability in terms of scope and maximum rewards. They will also share part of their rewards with their Voters, as seen in the example below, where:

- `CM_n` is Council Member `n`
- `V_i` is Voter `i`

**Note:**
Jsgenesis votes will not "count" when calculating these rewards.

#### Example
Suppose the recurring reward for each CM this term was USD 60.
The Council election had the following "own" `stakes` and `votes`, excluding Jsgenesis votes:
- CM_1: 5k
  - own: 2k
  - V_1: 3k
- CM_2: 5k
  - own: 5k
- CM_3: 11k
  - own: 4k
  - V_1: 2.5k
  - V_2: 4.5k
CM_4,5,6=CM_X
- CM_X: 3k
  - own: 3k
Total: 30k

At the end of their term, the KPI payout was USD 300. Half of that is split equally (150/6=25), half is divided by the stake.

- CM_1: `(60+25+(150*2/30))=95`
- CM_2: `(60+25+(150*5/30))=110`
- CM_3: `(60+25+(150*4/30))=105`
- CM_X: `(60+25+(150*3/30))=100`
- V_1:  `150*(3+2.5)/30=27.5`
- V_1:  `150*4.5/30=22.5`
-> USD 660

---

Note that the KPI rewards will be based on the exchange rate at the **START** of the Council's term.
The weekly "Recurring Rewards", will thus act as a constraint on the Council's budget.

If they overspend, their KPI rewards will go down in value. Assuming the exchange rate drops 20%, the KPI reward of USD300 will instead be USD240.

When a KPI is paid out (in tJOY), the corresponding amount will be added to the fiat pool.

## Get Started
Unlike most of the other current and future roles on the Joystream Platform, most of the information and actions required by participants in the governance system is available in our UI - named [Pioneer](https://testnet.joystream.org). For elected CMs, some familiarity with [GitHub](https://github.com/Joystream/community-repo/) is required, and at any time, a subset of the CMs must be able to use git, and basic coding review skills. As the project grows, new skills and more advanced skills may be required.

If you want to get elected as a CM or vote on the platform, you need to be a Member. Instructions for registration can be found [here](https://github.com/JoyStream/helpdesk/#get-started).

**Note**
After introducing `Memberships` to the platform, we found it to be confusing to have a concept of both `Accounts` and `Memberships`. We are in the process of renaming the `Accounts` to the `Keys`, but there are still traces of `Accounts` showing up.

# Council Elections
A new Council of CMs are elected at regular intervals. The election is decided by selecting the applicants that has the highest total "stake" backing them. Staking here means "locking" up your tokens, making them unusable for transfers or staking in other ways, thus forcing participants to put "skin in the game". The total stake is the sum of the applicant's own stake required to put themselves up for election, and the stake of any voters voting for them.

The terms of these elections are defined by some parameters. Although these can be changed either by the [Proposal system](/proposals), or by `sudo`, the parameter changes should be both infrequent and small.

The current set of parameters, as well as the status and stage of the [Council/election cycle](#council-election-cycle) can be found [here](https://testnet.joystream.org/#/council).

## Parameters
In addition to the length (and definitions) of the election stages described below, the most important parameters are:
- `Council Size`
  - This is the number of CMs that will be elected. This is a fixed value, meaning neither less nor more CMs can be elected.
- `Candidacy Limit`
  - This is the maximum number of applicants, that have [announced](#announcing) their candidacy, that are eligible to be voted for in the [voting](#voting) stage. This number will always be bigger than the `Council Size`
- `Minimum Council Stake`
- `Minimum Voting Stake`
  - The minimum stake that applicants and voters are required to put up, for standing as a candidate and voting (for others or themselves) respectively.

The full details of the election cycle will also expand upon these parameters.

## Council Election Cycle
The election cycle consists four stages. Currently, the length of each are:
1. [Announcing](#announcing) - lasts 28,800 blocks (~48h)
2. [Voting](#voting) - lasts 14,400 blocks (~24h)
3. [Revealing](#reveal) - lasts 14,400 blocks (~24h)
4. [Term](#term) - lasts 144,400 blocks (~10days)

### Announcing
During the entire `Announcing` stage, anyone that is a Member and can stake a greater number of tokens than the `Minimum Council Stake`, can apply to become a CM.

#### How to Announce
With your membership key:
- select "Council" in the sidebar
- click the "Applicants" tab
- set the amount of tokens you want to stake
- click "Apply to council" and confirm

**Important Notes**
- you can add to your stake later, by following the same approach as above
- this can be particularly useful because of the `Candidacy Limit`, which limits the number of applicants that goes through to the [voting](#voting)
- active CMs can "re-use" their own stake from the last election cycle
- this means that you if you staked 10k JOY on yourself, and have 5k "free" balance, you can stake 15k

#### End of Announcing
At the end of the stage, there are three outcomes depending on:
- the number of `Applicants`
- the `Council Size`
- the `Candidacy Limit`

##### Scenario A:
If: `Council Size <= Applicants <= Candidacy Limit`. I.e. the number of applicants is between the `Council Size` and `Candidacy Limit`.

The `Announcing` stage ends, with all the applicants proceeding to the `Voting` stage.

##### Scenario B:
If: `Candidacy Limit < Applicants`. I.e. the number of applicants is greater than the `Candidacy Limit`.

All the applicants are sorted and ranked by their stake. The `Announcing` stage ends, and only those with a rank better than, or equal to, the `Candidacy Limit` will proceed to the `Voting` stage.

The applicants that did not make it to the `Voting` stage get their stake back right away.

##### Scenario C:
If: `Applicants < Council Size`. I.e. the number of applicants is smaller than the `Council Size`.

There are not enough applicants to fill the Council slots, and a new `Announcing` stage begins, with all the applicants automatically re-entered.

### Voting
As soon as the `Announcing` stage closes, anyone that is a Member and can stake more than the `Minimum Voting Stake`, can vote for any of the applicants for the entire duration of this stage.

#### How to Vote
With your membership key:
- select "Council" in the sidebar
- click the "Applicants" tab
- find your preferred Applicant, and click the "Vote" button
- set the amount of tokens you want to stake
- click "Submit my vote" and confirm

You can vote as many times as you like, for any Applicant (including yourself).

**Important Notes**
When you submit a Vote, a `Random salt` will be generated for you, and only a `Hash` of the vote will be broadcast and stored on a chain. This means:
- no one will know who you voted for, or how much you staked
- unless this hash is "revealed" during the [Revealing](#revealing) stage, the vote will not count
- unless you save the `Random salt` somewhere, you will only be able to "reveal" your vote if:
  - you use the same key, computer and browser - without clearing local storage.
  - if you save the `Random salt`, you only need the key
- if you voted for one or more active CMs, you can "re-use" your voting stake from the last election cycle
- this means that you if you staked 10k JOY voting a one or more current CMs, and have 5k "free" balance, you can stake 15k for voting

### Revealing
As soon as the `Voting` stage closes, the `Revealing` stage begins. As stated before, only when a vote is "revealed" will it become public, and count.

#### How to Reveal
With your membership key (used to vote on the candidates):
- select "Council" in the sidebar
- click the "Votes" tab
- you should see the votes you have already made on this page
- click the "Reveal" button next to the votes you wish to reveal and confirm

#### End of Revealing
At the end of the `Revealing` stage, the applicants are sorted and ranked by their total stake, i.e. the sum of the stake(s) they bonded during the `Announcing` stage, and the sum of all **"revealed"** votes.

The applicants ranked within the number equal to the `Council Size` will become CMs.

The applicants that did not get elected will get their stake back immediately. The same goes for those that voted for them, and those that did not reveal their votes.

### Term
On the block that marks the end of the `Revealing` stage, the elected CMs will automatically be given their new privileges. Namely, the right to vote on [Proposals](#proposals), and be assigned an on-chain [Recurring Reward](#recurring-rewards).

The CMs' stakes will be not only be held until the `Term Duration` expires, but until a new Council is elected. The same applies to those that voted for them.

The Recurring Rewards however, will only be paid during the `Term Duration`.

Note that the next `Announcing` stage will start at the exact block the `Term Duration` expires.

# How to Get Elected
Unless you have sufficient tokens to get (re-)elected without any extra voters, you are unlikely to get any votes without making an effort to do so. As Jsgenesis represents a large proportion of the voting power, and community members are unlikely to vote for unknown actors without a proven track record, there are some steps you can take to greatly increase your probability of getting votes:

## Announce on the Forum
Before a new `Announcing` stage begins, a new thread will be made on the on-chain [forum](https://testnet.joystream.org/#/forum). Regardless of whether you are a new to the project, have been following it from a distance, are an active member or an experienced CM, make a post or two explaining why you deserve to be voted in. Some suggestions of what to include are:
- All
  - A little bit about yourself (no need to dox yourself)
  - Handles on other platforms, such as GitHub, Telegram, Discord, Keybase (again, no need to dox yourself)
  - Why you want to be a CM
  - Interest in the project
  - Interest in the space (blockchain, media, both)
  - Any useful skills or assets, such as:
    - technical/coding
    - sysadmin
    - economics
    - spreadsheets
    - math
    - media production, curation
    - free time and grit
    - etc.
- Newcomers
  - A little (more?) about yourself (still, no need to dox yourself)
  - What brought you in to the project
  - Goals
  - Participation in other projects of any kind
  - What you have done to prepare
  - Any questions about the role
  - etc.
- Long time community members
  - General Joystream "record", such as
    - Roles you had
    - Contributions (bounties, KPIs, etc.)
    - Proposals made
    - Participation on discussions on telegram, discord, forum, github, proposals
  - CM "record"
    - Election history
    - Proposal voting history
    - Council KPIs performed

As you are likely to get some follow-up questions, it is a good idea to check in at regular intervals to answer these.

# Elected Council Members
The CMs have a variety of [tasks](#tasks-overview). Some are pro-active, others are re-active. Some are recurring and predictable, others will require on the spot problem solving.

To some extent, the same applies to their rewards. They receive a fixed (in tJOY) [Recurring Reward](#recurring-rewards), which will be handled automatically by the chain. The other relies on their ability to solve the tasks and challenges they face through the [Council KPIs](#council-kpis).

A CM that is slacking off, or for other reasons unable or unwilling to perform their tasks will still receive their rewards for the term, but are unlikely to get re-elected in the near future.

## Tasks Overview
The CMs will be evaluated based on how well they perform these tasks. They are free to organize themselves in order to tackle specific tasks, or monitor different parts of the platform. If so, they should disclose it publicly, so that voters can evaluate their performance.

The list below contains a high level overview of their responsibilities:
- Elect a [Council Secretary](#council-secretary), to be the "official" point of contact between the Council and Jsgenesis
- Pay attention to the forum and [Discord group](https://discord.gg/DE9UN3YpRP), to assist and answer questions when appropriate
- Pay attention to incoming Proposals, discuss and make informed votes
- Monitor the performance on the [Working Groups](#managing-the-working-groups) and, if necessary, take action
- Monitor, communicate with, fund and report on the [forum sudo](/README.md#on-chain-forum)
- Monitor the platform's infrastructure, and report issues or perform the appropriate action(s)
  - endpoint nodes (does blocks come in on hosted pioneer)
  - pioneer (any sites not responding as expected)
  - storage system (is media served)
  - [status-server](https://status.joystream.org/status)
- Monitor the platform's spending and resource allocation
- Perform and/or delegate the required tasks related to the [Council KPIs](#council-kpis)
- Perform the required tasks related to the [Community Bounties](#community-bounties)

## Council KPIs
For each Council Term, a set of Council KPIs will be released. These will contain tasks that the Council, or individual CMs acting on behalf of the Council, should try to complete. Although the tasks and actions required by the Council will vary, the structure of the Council KPIs are fixed.

##### Structure Example
An example of the structure for a single Council KPI is outlined below. Note that the number of KPIs, success events, individual and sum of the rewards, and complexity of the KPIs per term will vary.

Council KPI - Term `X`
- `id:` - The unique identifier (eg. `X.1`)
- `Title:` - The title
- `Reward:` - The maximum reward paid, assuming all `Success Events` are delivered and graded complete
- `Description:` - A description of the problem solved if all `Success Events` are complete
- `Success Events:`
  - `1.` - A precise definition of subtask `1.`
  - `2.` - A precise definition of subtask `2.`
  - ...
  - `n.` - A precise definition of subtask `n.`
- `Annihilation:` - A precise definition of something that, if it occurs, would result in the entire KPI `Reward` getting lost, even in the event all the `Success Events` are fully completed.
- `Grading date:` - A (loose) deadline for when Jsgenesis will grade the KPIs, and if applicable, pay the CMs their rewards.

In addition to these, there are some other information that may or may not be included:
- `Starting at:` - The exact block height (and approx. date/time) from which the KPI is "Active"
- `Ends at:` - The exact block height (and approx. date/time) from which the KPI is no longer "Active"
- `Measurement period:` - Similar to the above

The reason these may not always be present is that the intention is that a Council KPI will be active from the block the Council is elected, until the block a new one replaces them.

### Scope of Work
The Council KPIs will emphasize tasks that the Council would be expected to handle or directly delegate once the project is live on mainnet. Instead of partially repeating what is listed [here](#tasks-overview), this section will instead focus on some examples of specific `Success Events`, and workflow.

Most KPIs will be graded based on one of two things:
1. A deliverable submitted
2. On-chain records and numbers

#### Council Deliverables
For a deliverable to qualify, it must, unless noted otherwise:
- Be submitted as a pull request ("PR") to the [community-repo](#https://github.com/Joystream/community-repo/)
- Either be made by the [Council Secretary](#council-secretary) directly, or reviewed and "approved" by said person
- Be Accompanied by a link to an "approved" [text Proposal](#proposals)

Unless these conditions are met, Jsgenesis reserves the right to consider a deliverable invalid. However, exemptions can be made depending on the circumstances.

It is irrelevant whether the Council collaborates in producing the deliverable, if it is made by a single CM, or procured from another Member or outsider. The only exceptions are if the deliverable:
- includes a claim (optional) of its source that proves false
- does not follow the license requirements of the repo, or violates any other license
- contains anything violating the platform [ToS](https://testnet.joystream.org/#/pages/tos)

#### Chain Values
The KPI will define whether the value in question shall be:
- maintained throughout some period of blocks
- reached at some point during some period of blocks
- the value from a specific block height

### Reports
Each Council will be prompted to submit deliverables reporting on things like:
- interesting events (such as Proposal history)
- discussions that lead to decisions made (such as voting on said Proposals)
- budgets and accounts
- network statistics

### Council Secretary
The Council Secretary is an informal role, where the Council themselves are given some flexibility in deciding on compensation and extending their Scope of Work, outside what is defined in the Council KPI.

The following bullet points should be expected as the `Success Events` for the KPI:
- A Text [Proposal](#proposals) electing an active CM is "approved" within 24h of a new Term
  - An optional deputy can be chosen
- The Secretary provides a GitHub handle, which will be granted ["Triage"](https://docs.github.com/en/github/setting-up-and-managing-organizations-and-teams/repository-permission-levels-for-an-organization) permission to the [community-repo](#https://github.com/Joystream/community-repo/)
- Secretary uses their permission to perform the tasks listed [here](#council-deliverables) and [here](#council-deliverables).

### Managing the Working Groups
Currently, there are two Working Groups on the network:
- [Storage Providers](/roles/storage-providers)
- [Content Curators](/roles/content-curators)

The role of the Council is not to control these directly, but rather ensure they are being well-run by their respective Leads. What is considered "well-run" is of course open to a wide interpretation, so specific quantitive and qualitative targets would be defined in the [Council KPIs](#council-kpis).

However, to understand what these targets could entail, how to monitor them, and perhaps even stay ahead of the curve, one should be familiar with some indicators of what to look for.

Finally, a CM must understand what the Council's options are for dealing with a Working Group that is underperforming.

#### Cost Control
How the Council chooses to approach this is up to them. It is up to the Lead of each group to create [Proposals](#proposals) for replenishing the Working Groups mint, but it's up to the Council to approve or reject these requests.

A good approach could be to agree on weekly budgets, and revise them on an as-needed basis. How to set these budgets would depend on a variety of factors such as:
- Changes in the exchange rate
- Increased costs and/or workload
  - The Storage Provider Group's real costs depend on:
    - size of the `dataDirectory`
    - bandwidth due to frequent uploads, downloads and playbacks
    - replication requirement (the platform may wish to have sufficient backup in case workers quit or crash)
    - changes in hardware/VPS costs
  - The Content Curators Group's costs is mostly associated with their time:
    - Verifying new content are in line with the [ToS](https://testnet.joystream.org/#/pages/tos)
    - Verifying the metadata of new and existing content
    - Running or creating tools for monitoring changes in the Content Directory or `dataDirectory`

#### General Performance
In addition to the bottom line costs, there are some nuances to the distribution of said costs, and the general quality of the service each Working Group Provides.


**Storage Providers**
- Quality of service
  - Is the Storage Providers' uptime acceptable and consistent
  - Are uploads interrupted or failing at an unacceptable rate
  - Is the content replicated to an acceptable level
- Speed of service
  - Are some/all providers slow to upload to
  - Are some/all providers slow to download/play from

**Content Curators**
- Quality of service
  - Is good at getting content featured or promoted
  - Are quality channels getting `verified`
  - Are the curation actions made accurately and reliably
- Speed of service
  - Are the points listed above dealt with in a reasonable time
  - Are the curators responsive to requests/complaints/questions made

**Lead Actions**
Are the Leads doing their jobs, in terms of:
- Managing workers
  - slashing and/or firing non-performing workers
  - keeping the "right" workers, when a cut to the number of workers is required
  - creating and completing new openings quickly and professionally
  - hiring/firing too many/few workers
- Professionally Conduct
  - reacting swiftly to requests/complaints/questions made
  - failing to report their actions as/if required
  - responding to the Council's directives
- Economics
  - ensuring the workers' stakes and unstaking terms are reasonable
  - creating the proposals to replenish their mints in time

#### Council Actions
In some cases, the Council may wish to take some action in relation to the Lead of a Working Group.

If a Working Group is not performing adequately, the first course of action may simply be to give an informal warning to the Lead in question.

The main way of dealing with Leads is through the [proposal system](#proposals). Unfortunately, there are currently limited ways of dealing with the Curator Lead. For the Storage Lead, there are more options, but only one that is not a punishment:
**Content Curator Lead**
- reduce the group's mint
- fire the lead
**Storage Provider Lead**
- reduce the group's mint
- slash all or parts of the Lead's stake (without firing them)
- fire the Lead (without slashing them)
- fire and slash all or parts of the Lead's stake
- decrease the stake of a Lead (in case the exchange rate has made the stake bigger than "justifiable")

### Managing Community Bounties
The concept and some examples of Community Bounties (previously referred to as "Community KPIs") are explained [here](/community-bounties), so this section will rather focus on the Council's role in these as Project Managers. What this entails exactly will vary depending on the type, complexity, and stage of the active Community Bounties themselves, but "good" Project Management will be rewarded through the [Council KPIs](#council-kpis).

A Community Bounty will in general be graded based on deliverables, with conditions similar to what is described [here](#council-deliverables).

Unlike the Council KPIs, the rewards for fulfilling them will not go directly to the CMs, but rather increase the [Fiat Pool](/tokenomics/README.md#fiat-pool), thus increasing the value of all the token holders. However, it's assumed that most, if not all, of these rewards will be directed at the group or individual that made the deliverable.

#### Reward Distribution
The Council decides how much of the total Bounty reward will go to the Submitter, if the rewards should or can be split, and so forth.

#### Format
The format should try to optimize for the time, quality, risk and cost, associated with each Bounty. The  [Closed](#closed), [Free For All](#free-for-all) and [First Come, First Served](#first-come-first-served) formats presented are just suggestions.

##### Closed
For a Bounty that requires investing lots of time and/or other resources, it may be reasonable to guarantee one or more Appliers that gets Assigned some time to complete all, or some, of the work, without having someone come in and "snipe" the reward.

##### Free-For-All
For smaller, and perhaps more creative and subjective Bounty, it may make more sense to leave it as a "free-for-all". In this case, the Council sets a deadline, picks the best Deliverable(s), and rewards the Submitter(s) as per the rules.

##### First Come, First Served
For smaller, perhaps more time sensitive Bounty, one could choose a format where anyone can enter, but each Submitter's Deliverable is reviewed by the chronological order they are submitted. The first acceptable Deliverable(s) is granted the reward(s).

##### Other
In addition to the varieties outlined, other formats can be defined and chosen if they are more appropriate for a specific Bounty.

A "new" Council must honor any agreements and rules set by their predecessors, for as long as the rules say so.

#### Workflow
The workflow will depend both on the [Reward Distribution](#reward-distribution) and the [Format](#format), and must be established beforehand.

- For "Closed" formats, an Applier must present a bid why they should be assigned the given Bounty. This should include detailed terms, such as time needed, costs, etc. If approved, this makes the terms valid.
- In some cases, it may make sense to break a Bounty up in to milestones, with partial rewards at each stage. These builds trust as the Council can see the progress being made, and the Assignee can get chunks of the reward along the way.
- In other cases, the person may need some initial funding to get started.
- For "Closed" formats, the specifics of the workflow could be part of the Applier's application for participation.

#### Steps

##### 1. New Bounty Made
Although the Council decides on the rules and reward distribution, they listen for input from others in the platform forum and on Discord. Within a reasonable time (as stated in the Council KPI), the rules for the Bounty are presented in Text Proposal, voted through, and published on GitHub.

##### 1.5. Work is Assigned
Depending on the rules chosen, there may be a step to assign the work to one or more Assignees.

This will require some back and forth through multiple Proposals, and should thus be avoided for less complex Bounties.

##### 2. Work Happens
For a "Closed" format, it can mean a series of Text and Funding Proposals, waiting, and ongoing communication between the Assigned/Assignees, and the CMs.

For a "Free for All", it can be mean reviewing submitted Deliverables as they come in, or waiting for the deadline. How a Submitter should make the CMs aware of their Deliverable once ready (GitHub, Discord, forum or Proposal) must be defined in the rules. A "First Come, First Served" format will be similar to the "Free for All". Once one or more Deliverables are approved, the Submitter(s) should be considered as Assigned in Step 3.

##### 3. The Work is Submitted to the Council
Regardless of format, once an Assignee, or otherwise qualified Submitter, considers their work done, they create a (final) Spending Proposal, which in total rewards them the agreed amount, links to all relevant discussion and rules, and a link to their work.

Once the Council considers the Deliverables complete, this final Spending Proposal is "approved" and successfully executed.

##### 4. Jsgenesis Grading
After Step 3, the Submitter has received their reward, and their work now "belongs" to the platform.

If the Deliverable is to be submitted to the [community-repo](https://github.com/Joystream/community-repo/), the Council Secretary approves the pull request. Regardless, the Secretary must notify Jsgenesis.

Jsgenesis will then review and grade the Deliverable as such. This can result in a reward anywhere between nothing (failed), or everything (full score), and the fiat pool will be increased accordingly.

It may be that this reward is smaller than that which was rewarded to the Submitter. This will in some cases cost the token holders, and in other cases be deducted from the Councils KPI rewards. Regardless, the Council will likely be punished.

#### Councils Role
As seen in the workflow, the Council's role in the Community Bounties is substantial. They will work as the Project Managers, and are at the end held accountable for the quality of the Deliverable they submit for grading. These tasks may be a formal part of the Councils KPI directly, but the efficiency, creativity, rules, workflow, speed and outcome of the process will anyway be part of the Jsgenesis Council voting process.

To avoid making this longer than necessary, and hopefully let a system emerge naturally, no examples are included.

# Governance
Constantinople introduced a number of important changes to the governance structure of the platform. The most important of these was the enhancement of the platform's proposal system. You can read descriptions of each of the proposal types on the helpdesk article [here](/proposals/README.md).

Most of the proposals are meant to allow the Council to allocate the platforms resources as efficiently as possible. In order to do so, a [tokenomics spreadsheet](https://docs.google.com/spreadsheets/d/13Bf7VQ7-W4CEdTQ5LQQWWC7ef3qDU4qRKbnsYtgibGU/edit?usp=sharing) has been made to assist in the decision-making.

## Proposals
As a Member (CM or not) you are able to make proposals to be voted on by the Council.

The types of proposals available include:
- Text/signal Proposal
- Spending Proposal
- Set Max Validator Count
- Set Content Curator Lead
- Set Content Working Group Mint Capacity
- Set Election Parameters
- Runtime Upgrade
- Add Working Group Leader Opening
- Set Working Group Mint Capacity
- Begin Review Working Group Leader Application
- Fill Working Group Leader Opening
- Slash Working Group Leader Stake
- Decrease Working Group Leader Stake
- Set Working Group Leader Reward
- Terminate Working Group Leader Role

To make a proposal:
1. Click the Proposals tab in the Pioneer sidebar (`/proposals`).
2. This will provide a view of all the currently active (as well as past) proposals.
3. If there are fewer than five `active` proposals, you can click the `New Proposal` button at the top of the page.
4. You will be given a list of proposal types; select the one which is required for your proposal.
5. Make a note of the staking requirements, ensuring your account balance is sufficient to create the proposal.
6. Also note the other variables on the page, paying particular attention to the quorum and threshold for votes.
7. Click `Create Proposal` and fill in the required fields, `Title`, `Rationale` and `Description`.
8. When you are ready, click `Submit Proposal` and sign the transaction.
9. If everything has worked correctly, your proposal should now be `active` on the proposals page.

## Voting on Proposals
While any member can make a proposal, only Council Members can vote!

The voting process is rather simple. The first step is to navigate to the proposals (`/proposals`) page and view the currently active proposals. Select the proposal you would like to vote on and simply click the button corresponding to your decision (based on discussion with other council members) on the merits of the proposal.

You can choose:

- `Approve` - approving the proposed action
- `Reject` - reject the proposed action
- `Slash` - reject the proposed action, and slash the stake of the proposer
- `Abstain` - abstain from voting

More information on how council votes are processed can be read [here](/proposals/README.md).
