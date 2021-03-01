# Launch of Alexandria

Alexandria was launched as a new chain on the 21st of September 2020, effectively deprecating [Constantinople](/testnets/constantinople).

## Migration
A lot of the state and "history" was migrated from Constantinople:
- All memberships
- Most balances`*`:
  - all those associated with a membership `root` or `controller`
  - all tokens staked for [Council Members](/roles/council-members) and their voters, but as "free" balance
  - all tokens staked for (as "free" balance), and the balance of the "role" key of, active [Content Curators](/roles/content-curators) and [Storage Providers](/roles/storage-provider)
  - all tokens staked in [Proposals](/proposals)
  - all tokens staked for [Validators and Nominators](/roles/validators), although slashed tokens was deducted
- The [Forum](/README.md#on-chain-forum)
- Old [Proposals](/proposals) history and discussions, although only in "viewable" in [Pioneer](https://testnet.joystream.org/#/proposals/historical)
- All Channels and content
- The [Fiat Pool](/tokenomics/README.md#fiat-pool)


`*`
- The `Total Issuance` at the snapshot was: 154289593 tJOY
- The `Total Exported Issuance` was: 140539804 tJOY
- "Lost" tokens: 13749789 tJOY

If some of your tokens were "lost" in the transfer, you can "claim" these until the end September 2020.

## Changes
After the upgrade, all roles, e.g. `Validators`, `Storage Providers`, `Council Members` and `Curators` were fired from their position.

In addition, the old KPI scheme was replaced by [Council KPIs](/tokenomics/README.md#council-kpis) and [Community Bounties](/tokenomics/README.md#community-bounties).
