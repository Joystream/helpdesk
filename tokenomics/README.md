Overview
===

This page will explain the token economics ("tokenomics") of the Joystream testnets, and how this applies to the individual actors, and platform as a whole.

Table of Contents
---
<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
- [Tokenomics](#tokenomics)
  - [Token Issuance](#token-issuance)
    - [Inflationary Forces](#inflationary-forces)
    - [Deflationary Forces](#deflationary-forces)
  - [Fiat Pool](#fiat-pool)
    - [Regular Replenishments](#regular-replenishments)
  - [KPIs and Bounties](#kpis-and-bounties)
    - [Council KPIs](#council-kpis)
    - [Community Bounties](#community-bounties)
  - [Tokenomics Examples](#tokenomics-examples)
    - [Example A](#example-a)
    - [Example B](#example-b)
<!-- TOC END -->

# Tokenomics
At launch of a new testnet, the token (tJOY) issuance will be set/calculated, and an initial USD denominated fiat pool will be created to back it. The key concept is outlined below:

- All roles will be rewarded directly in tJOY
- tJOY will be backed by a USD fiat pool and redeemable via Bitcoin Cash at the convenience of participants
- This means that tJOY - only needed for staking and fees on the previous testnet - will now function more like the mainnet token
- The exchange rate will simply be amount of tokens issued divided by the size of the fiat pool
- When a user exchanges their tJOY for USD, the tokens will be burned immediately, thus **not affecting the exchange rate**
- New tokens rewards are minted to pay for the various roles on the network
- The fiat pool will be topped up regularly for every new Council Term, without minting new tokens, effectively increasing the exchange rate (all else being equal)
- For every new Council term, Jsgenesis will create [Council KPIs](#council-kpis), each assigned a USD value. If the goals are achieved, Jsgenesis will reward the Council without affecting the exchange rate
- Jsgenesis will also create [Community Bounties](#community-bounties), similar to bounties, but managed by the Council. These are also assigned a USD value, and if achieved, Jsgenesis will (indirectly) reward the individual or group that achieved the goals.

Examples of the system through the eyes of a user can be found [here](#tokenomics-examples). In order for community members to get a grasp of the tokenomics, a [spreadsheet](https://docs.google.com/spreadsheets/d/13Bf7VQ7-W4CEdTQ5LQQWWC7ef3qDU4qRKbnsYtgibGU/edit?usp=sharing) has been made.


## Token Issuance

The issuance of new tJOY will in practice be a cost incurred for all holders of tJOY, both passive and active (with the exception of tokens minted for [KPIs](#kpis) achieved). Because of this, it is in the interest of all holders to ensure the platform's resources are well managed, and keep tabs on the [Council Members'](../roles/council-members) spending.

Jsgenesis will try to mimic the market forces of supply and demand, by rewarding good behavior through [KPIs](#kpis), to ensure participants have incentives to keep the platform and associated infrastructure running.

### Inflationary Forces
There are many inflationary forces in the network, but not all of them will impact the exchange rate. The main ones are recurring rewards, and other costs associated with achieving KPIs.

- Recurring rewards, currently paid to:
  - [Council Members](/roles/council-members) for running and managing the platform's day-to-day operations
  - [Storage Providers](/roles/storage-providers) for receiving, storing and serving content files
  - [Content Curators](/roles/content-curators) for monitoring and curating content and channels
- Automatic rewards, to [Validators](/roles/validators) and [Nominators](/roles/validators/README.md#nominating) are minted as rewards for finding blocks, and keeping the network up and running
- [Spending Proposals](/proposals/README.md#spending) that are "approved" and executed

Tokens will also be minted for other purposes, such as faucets, competitions, [KPIs](#kpis), etc. Unlike the costs listed above however, these will under normal circumstances be offset by an equivalent increase of [Fiat Pool](#fiat-pool).

If the system is changed, some of these can impact the exchange rate in the future, but users will be warned in advance.

### Deflationary Forces
Tokens are slashed and/or burned for a variety of reasons, thus reducing supply and increasing the exchange rate.

- Transactions (aka. extrinsics) fees, are burned
  - Extrinsics are now in most cases free, but
  - Users may need/choose to set a higher fee for transaction priority
  - Users, or Jsgenesis, may set high fees to intentionally burn tokens
- Creating [Proposals](/proposals) requires the creator to put up [Stake](/proposals/README.md#stake) (the size depends on the perceived "severity" of the Proposal type). Unless the Proposal gets [Approved](/proposals/README.md#approved), the full amount will not be returned to the "creator":
  - A [Slashed Proposal](/proposals/README.md#slashed) means slashing and burning the entire Stake of the "creator"
  - A [Cancelled Proposal](/proposals/README.md#slashed) means a fixed amount of the Stake is burned
  - A [Rejected Proposal](/proposals/README.md#rejected) means a smaller, fixed amount of the Stake is slashed and burned
  - An [Expired Proposal](/proposals/README.md#expired) counts as "rejected"
- Slashing Staked [workers](/roles). The mechanism of these slashes depends on the role, but in all cases, the tokens are burned.
  - [Validators](/roles/validators) (and their [Nominators](/roles/validators/README.md#nominating)) get slashed automatically by the chain if they go offline, or respond too slowly, without first stopping.
  - [Storage Providers](/roles/storage-providers) can get their stakes slashed by their Lead.
  - The [Storage Lead](/roles/storage-lead) can get their stakes slashed by the Council through a [Proposal](/proposals/README.md#slash-working-group-leader-stake).
  - [Content Curators](/roles/content-curators) can get their stakes slashed by their Lead.


When an exchange takes place, the tokens are also burned, but this will have no impact on the exchange rate as the fiat pool will decrease proportionally.

## Fiat Pool
The fiat pool, denominated in USD, will start at a set value, but will change continuously.

### Regular Replenishments
For each Council Term (currently 2 weeks), an amount of USD will be added to the fiat pool as recurring replenishment, thus increasing the value of each token, if one were to assume the issuance would stay constant.

## KPIs and Bounties
Jsgenesis will regularly release new Key Performance Indicators ("KPIs") and Bounties as a way to incentivize the community and its participants to perform certain actions, maintain network functionality, produce reports, assets, code or other deliverables, etc.

The KPI scheme has evolved over time, and further changes in the future should be expected.

Currently, we separate these as two different types, [Council KPIs](#council-kpis) and [Community Bounties](#community-bounties), each with a distinct structure, frequency, scope, and reward mechanism.

### Council KPIs
For each new Council elected, a fresh set of Council KPIs are published by Jsgenesis. These KPIs will mainly serve to incentivize the Council Members to manage the platform, pay attention to the Tokenomics, monitor the network and respond to proposals and other requests.

Each individual KPI in the set will:
- contain some defined tasks or conditions for the Council to address or deliver
- have a specific maximum reward assigned to it (in USD)
- (usually) last during the entire Term of the Council
- be graded (individually) a few days after the end of said Term

The sum of the rewards earned will be given directly to the individual Council Members, and those that voted for them, without affecting the overall exchange rate, by topping up the [Fiat Pool](#fiat-pool) and minting new tokens.

As the Council KPIs mainly apply to prospective Council Members, the full details can be found under their role section [here](/roles/council-members/README.md#council-kpis).

### Community Bounties
The Community Bounties are meant to replace the "old" bounty system previously used by Jsgenesis. In discussions with the community, these have been referred to as "Community KPIs", but we've chosen to use the term Community Bounties to properly distinguish them.

Jsgenesis will publish these in a format similar to that of a [Council KPI](#council-kpis), but with some key differences:
- They will not be published at the same regular and predictable intervals
- They will not necessarily have deadlines
- Jsgenesis will rarely get involved in managing or assigning them

The last part is key, as the Council will act as Project Managers, and serve as a bridge between Jsgenesis and the individual or group working on them.

#### Types of Tasks
The tasks associated with these Community Bounties will ideally try to solve some problem either for the community or Jsgenesis, but in some cases, their main purpose will be to create some fun and/or attract new members to the community.

Over time, the tasks should allow people with different skillsets and interests to participate. Most challenges will be easier if you have some technical or creative skills, but in other situations it will simply require putting in some time and effort:
- Coding
  - Discord/Telegram bots
  - Scripts
  - Enhance the UI
  - Improve infrastructure
- Writing
  - Documentation
  - Marketing material
  - Explainers
  - Translations
- Creative
  - Videos
  - Artwork
  - Gifs
  - Memes
- Research, testing and sourcing
  - Source/upload freely licensed media
  - Testing and benchmarking tools
  - Research interesting projects
  - Tokenomics research
- Reviewing
  - All of the above

More details about Community Bounties can be found [here](/roles/builders).


## Tokenomics Examples

A rational user will continuously consider their options, and try to maximize their profits based on a variety of inputs such as:
- tJOY holdings
- the tJOY costs and returns associated with the available roles
- the USD costs of hardware, electricity and their time
- opportunity costs
- exchange rate changes from
  - tJOY issuance change
    - recurring role rewards
    - fees
    - slashes and tJOY burns
    - `Council` spending
  - fiat pool inflows and outflows
    - replenishment of fiat pool
    - KPIs achieved leading to an increased fiat pool

### Example A

Suppose there is `10,000 tJOY` in circulation, and `USD 1,000` represents the initial fiat pool. This means that the exchange rate is `0.1 tJOY/USD`.

A user has `1,500 tJOY`, and after weighing their options and calculating the rate, they decide to cash in `500 tJOY`. They go to [the incentives page](https://www.joystream.org/testnet), verify the exchange rate, and follow the instructions on how to cash in. After submitting and signing the transaction, a new pending exchange is displayed at the bottom of said [page](https://www.joystream.org/testnet):

The Joystream transaction locks in the USD value of the exchange. At regular intervals, all pending transactions will be paid out in Bitcoin Cash, with the prevailing BCH/USD rate at the time of payout.

All else being equal, this will reduce the tJOY issuance from `10,000 to 9,500`, and the USD fiat pool from `1,000 to 950`. The exchange rate will therefore not be changed, and there is no incentive to start a run on the bank.

Furthermore, suppose the user, after considering their skillset and rate of return, decided that the best option for them was to stake their remaining `1,000 tJOY` for the role of `Storage Provider`, and assume further that the payout for this role was `2 tJOY per 3600 blocks` (6 hours).

Assuming again all else being equal, i.e. the only token inflation on the network was the payout for *this* user, the payout stays the same, and our user performs their job satisfactory, they can expect to cash in `560 tJOY` every week. After the first week, the total issuance is now `10,060 tJOY`, and the fiat pool is now `$950 USD`. The user cash out their `560 tJOY`, and with a rate of `~0.094 tJOY/USD`, will receive `$52.9 USD` for their job.

If the user had instead chosen to exchange all their `1,500tJOY` in the first place, they would have locked in a value of `$150 USD`. Their actual choice however, resulted in having cashed in a total of `$102.9 USD`, with another `1,000` tJOY worth `$94.4 USD` at the prevailing rates, for a total of `$197.3 USD`.

In practice, the system will be far more complex than what is outlined above. For more precise calculations, please use [the spreadsheet](https://docs.google.com/spreadsheets/d/13Bf7VQ7-W4CEdTQ5LQQWWC7ef3qDU4qRKbnsYtgibGU/edit?usp=sharing).

### Example B

After two weeks, suppose there is now `100,000 tJOY` in circulation, and `USD $3,000` in the fiat pool. This means that the exchange rate is `0.03 tJOY/USD`. However, the next replenishment of the fiat pool is set to `$200 USD`. Additionally, two `KPIs` are live, with a potential payout of `$100 USD` for each. These are both scheduled in exactly 7 days. The users have `4000 tJOY`.

Currently, the status of the roles and rewards are:

**Storage Providers**

-   5 slots filled, 1 slot open
-   Stake is `3500 tJOY`, cost of entering is `200 tJOY`
-   Rewards are `4 tJOY/600` blocks per slot
-   The users find that running a Storage Provider costs them `$4 USD per week`

**Validators**

-   All 10 slots filled
-   The lowest current stake in the pool is `2500 tJOY`
-   Rewards are `575 tJOY/100800 blocks` in total
-   The users find that running a Storage Provider costs them `$1 USD per week`

**Council Members:**

-   New election is running, with 6 slots
-   It is assumed `4000 tJOY` will be enough to earn a slot
-   Rewards are `300 tJOY/100800` blocks per CM

**Curator:**

-   The lead and 2 slots are filled, 1 slot is open for application
-   Stake required is `500 tJOY`
-   Rewards are `5 tJOY/3600` blocks per slot for curators
-   The lead earns `12tJOY/3600` blocks

The user assumes that on average, the KPIs will return 150 USD this week, and decides to calculate their estimated earnings for each option, assuming:

-   all slots fill up
-   no tx fees included
-   no slashing

At first glance it appears as if then `Storage Provider` is the most lucrative role. However, with a second look, one can see that you can instead try to become both a `Curator` and a `Validator`, as the up front stake and cost for the former totals `3,700 tJOY`, whereas the latter two totals just `3,000 tJOY`.

There are still a lot of factors that should be considered, such as time spent, transaction fees, risk of not getting or keeping your role, tokens being locked in for staking, reputation and knowledge building, etc. When all these are weighed against each other, one must assume that the various roles will be ranked differently depending on ones skills, costs, risk tolerance and other preferences.
