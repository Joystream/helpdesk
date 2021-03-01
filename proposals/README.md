Table of Contents
---
<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
- [Overview](#overview)
  - [Implemented Proposals](#implemented-proposals)
      - [Text](#text)
      - [Spending](#spending)
      - [Set Max Validator Count](#set-max-validator-count)
      - [Set Content Curator Lead](#set-content-curator-lead)
      - [Set Content Working Group Mint Capacity](#set-content-working-group-mint-capacity)
      - [Set Election Parameters](#set-election-parameters)
      - [Runtime Upgrade](#runtime-upgrade)
      - [Add Working Group Leader Opening](#add-working-group-leader-opening)
      - [Begin Review Working Group Leader Application](#begin-review-working-group-leader-application)
      - [Fill Working Group Leader Opening](#fill-working-group-leader-opening)
      - [Set Working Group Mint Capacity](#set-working-group-mint-capacity)
      - [Slash Working Group Leader Stake](#slash-working-group-leader-stake)
      - [Decrease Working Group Leader Stake](#decrease-working-group-leader-stake)
      - [Set Working Group Leader Reward](#set-working-group-leader-reward)
      - [Terminate Working Group Leader Role](#terminate-working-group-leader-role)
  - [Deprecated Proposals](#deprecated-proposals)
      - [Evict Storage Provider](#evict-storage-provider)
      - [Set Storage Role Parameters](#set-storage-role-parameters)
  - [Mechanics](#mechanics)
      - [Voting Kinds](#voting-kinds)
      - [States and Outcomes](#states-and-outcomes)
  - [Proposal Parameters](#proposal-parameters)
  - [Proposal Flow](#proposal-flow)
    - [Example](#example)
      - [Voting Scenario A](#voting-scenario-a)
<!-- TOC END -->

# Overview

When the `Council` was first introduced, it was only able to vote on whether a runtime upgrade should be implemented. This  rarely occurred, making the Council a rather insignificant part of the platform.

As the `Council` is meant to be the executive arm of the Joystream governance system, we are adding a proposal system that will allow the users to control most of the day-to-day decision-making on the platform.


## Implemented Proposals

The list below contains all the proposal types currently available.

#### Text
Aka. "Signal Proposal"

Although no action will happen if such a proposal is voted through, it provides a way for user to request changes, propose improvements, complaint about something, and in general voice their opinion on a matter. This will open a discussion, and Council Member can signal their approval or rejection through a vote. This can be used to notify the platform developers about key feature missing, highlight a topic of controversy, etc.

#### Spending
Aka. "Funding Request"

In general, this proposal will include an amount, and a beneficiary. This can be used in to fund development, pay winners of competitions, bonus payments for a role, or anything else that requires minting new tokens to a specific individual or group.

#### Set Max Validator Count
The Validators are rewarded for producing blocks, and will share the rewards that are minted each era (target 3600 blocks). This reward is calculated based on the total issuance, and the amount of tJOY staked by the pool of Validators relative to the total issuance. A higher number means smaller rewards for each individual Validator, but set to low, and the network grinds to a halt.

#### Set Content Curator Lead
The Content Curator Lead is the first implementation of the concept of Group Leads on the platform. These will in general be responsible for hiring, firing, rewarding and training the group they are leading. They are hired by the council, and will be given a budget to perform their role satisfactory, without inflating the supply more than necessary.

This means they have to answer to the users if they fail in their task. In this particular case, all members can propose to:

-   Set a Lead if there are none currently occupying the role
-   Fire the existing Lead, without setting a new one
-   Replace the existing Lead, with a specified new member

If the proposal is voted through, the change will occur immediately.

#### Set Content Working Group Mint Capacity
To avoid the Lead paying themselves too much, or frivolous spending in general, the Lead can only spend as much as the Mint Capacity. Effectively, a budget for their spending. Once the Mint runs out, recurring rewards for the Content Curators (including themselves) will be frozen.

If the Lead, or anyone else, wants to replenish or drain the existing Mint, a proposal can be made. If voted in, the new Capacity proposed will be set immediately.

#### Set Election Parameters
As the Council will see a significantly increased workload, there may be need to change the same Election cycle parameters. This proposal allows the Council to vote on expanding the Council seats, increase or decrease the length of the Voting process, or the minimum stakes required to participate. If this proposal is voted through, a change of these parameters will not be activated until the next election cycle, to avoid the current Council making changes benefiting themselves.

#### Runtime Upgrade
As before, upgrading the runtime can be proposed by any member, and voted in by the Council. This is a critical proposal that, if a "bad" runtime is proposed and voted in, can kill the blockchain.

#### Add Working Group Leader Opening

This proposal allows an opening for a Storage Lead to be created. When editing the "Opening schema", you must ensure your changes still returns a valid JSON schema. This determines what information is collected from candidates. Note that the reward specified is not binding, and is only determined when the [Fill Working Group Leader Opening](#fill-working-group-leader-opening) proposal is made (and approved).

#### Begin Review Working Group Leader Application

This simply sets the opening for Storage Lead to the "in review" status, meaning no further applications can be accepted. It is required to move on to the `Fill Working Group Leader Opening` proposal.

#### Fill Working Group Leader Opening

If the Opening is in the "Review Stage", use this proposal to propose a specific Lead. The Council can now vote, and, if approved, this will be the new Lead.

Note that there can be multiple proposals of this type at the same time, so multiple candidates can be considered simultaneously. However, once one is approved, the others will fail.

#### Set Working Group Mint Capacity

This effectively acts as a budget for the working group (currently referring to the Storage Working Group). The Storage Lead will be unable to spend more than the limit established by this proposal.

#### Slash Working Group Leader Stake

To punish or warn the Storage Lead for not performing their job correctly, they can be slashed partially or fully without firing them using this proposal type.

#### Decrease Working Group Leader Stake

This proposal type allows decreasing the stake of the Storage Lead.

#### Set Working Group Leader Reward

This proposal allows for changing the reward for the Storage Lead if it appears too little or too much. Note that only the amount can be changed, not the frequency.

#### Terminate Working Group Leader Role

If for whatever reason the Storage Lead needs to be removed from their post (and potentially slashed), this is the proposal type which needs to be voted on.

## Deprecated Proposals

#### Evict Storage Provider
This allows users to make a proposal to "fire" a Storage Provider that is not performing the role satisfactorily.

#### Set Storage Role Parameters
The Storage Provider will be paid by minting new tokens, effectively increasing the tJOY supply. The incentive will be to keep both the number of slots, and the size of the individual rewards, as low as possible while maintaining a sufficient service.

## Mechanics

#### Voting Kinds
A voter can choose between the following outcomes:
- `Approve` - approving the proposed action
- `Reject` - reject the proposed action
- `Slash` - reject the proposed action, and slash the stake of the proposer
- `Abstain` - abstain from voting

#### States and Outcomes
Below is a list of the states a proposal can be in, and what each of them means:
- `Active` - the proposal can be voted on, and no resolution has been made
- `Grace Period` - the proposal has been approved, and is awaiting execution
- `Executed` - the proposal was approved, and, after a potential `Grace Period`, executed on chain
- `Execution Failed` - the proposal was approved, and, after a potential `Grace Period`, attempted to be executed on a chain. For some reason, the execution failed
- `Rejected` - the proposal was rejected by the council
- `Slashed` - the proposal was rejected, and the stake of proposer was slashed by the council
- `Expired` - the council members did not reach consensus, and the proposal expired without any action. This can be the result of insufficient voter turnout, or disagreement between the council members

## Proposal Parameters
The parameters below are specific to each proposal type, and the values are chosen to balance the importance and risks associated with each of them.

- **Voting Period [blocks]** - the maximum amount of blocks where voting is open before a proposal expires
- **Grace Period [blocks]** - the amount of blocks after a proposal is approved until it as implemented on chain
- **Approval Quorum [%]** - the amount of votes required to be cast before a proposal _can_ be approved
- **Approval Threshold [%]** - the required threshold ratio of cast votes for `approve`, relative to those that vote `abstain`, `reject` or `slash`
- **Slashing Quorum [%]** -  the amount of votes required to be cast before a proposal _can_ lead to slashing the stake of the proposer
- **Slashing Threshold [%]** - the required threshold ratio of cast votes that slash relative to those that vote approves, abstain or reject.
- **Proposal Stake [tJOY]** - the required stake to create a proposal of this type

There are also some general parameters that applies equally to all proposals, such as fees, length of text allowed, the maximum number of proposals currently in the `active` stage, etc.

## Proposal Flow

Any member of the platform with a sufficient quantity of tokens to stake can create a proposal. If the proposal includes values that are within the allowable range, and there are fewer `active` proposals than permitted, the proposal was proceeded to the `active` state where the council can vote on it.

### Example

Suppose there are currently 20 members of the council. A proposal to [set max validator count](#set-max-validator-count) is made, where the parameters below apply:

| Proposal Parameters                | Value           |
|:---------------------------------:|:------------:|
|`voting_period`                  |  43,200        |
|`grace_period`                   | 0                  |
|`approval_quorum_percentage`    | 50%             |
|`approval_threshold_percentage` | 75%             |
|`slashing_quorum_percentage`    | 60%             |
|`slashing_threshold_percentage` | 80%             |
|`required_stake`                |  25,000            |

A member puts up the required stake of 25,000 tJOY, and the proposal goes the `active` stage at block height 100,000.

#### Voting Scenario A
The votes come in, until we have:

- 6 `Approve`
- 0 `Reject`
- 0 `Slash`
- 0 `Abstain`

At this point, the `Approval Quorum` parameter is fulfilled (100%>75% approval), but there are still too few votes cast to fulfill the `Approval Threshold` (at 30%<50%).

A few more votes are cast:

- 6 `Approve`
- 1 `Reject`
- 1 `Slash`
- 1 `Abstain`

At this point, neither the `Approval Quorum` parameter (67%<75% approval), nor the `Approval Threshold` (at 45%<50%), is fulfilled.

Another vote comes in:

- 6 `Approve`
- 2 `Reject`
- 1 `Slash`
- 1 `Abstain`

At this point, `Approval Quorum` parameter (60%<75% approval) is not fulfilled, whereas the `Approval Threshold` (50%), is now fulfilled.

A few more votes are cast:

- 8 `Approve`
- 2 `Reject`
- 1 `Slash`
- 1 `Abstain`

At this point, `Approval Quorum` parameter (67%<75% approval) is not fulfilled, whereas the `Approval Threshold` (50%), is now fulfilled.

A final vote for `Approve` is cast, and the
