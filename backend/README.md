# `Bourne bot`'s `REST API`

## Tech Stack

* `Nodejs` / `TypeScript`
* `Loopback 4`


# Design

The bot needs to be able to :
* `C.R.U.D.` `Hashicorp Vault` secrets
* `C.R.U.D.` `secrethub` secrets
* `C.R.U.D.` `Kubeseal` secrets
* `C.R.U.D.` the Mongo database of all identities
*
* prometheus exporter for both the bot and the REST API
* architecture :
  * a REST API to implement all vaults' standard ops (`C.R.U.D.`) in `Loopback 4`
  * a bot (which can be scaled) to run all REST API  standard ops (`C.R.U.D.`) from (one bot for each chatops) :
    * `Slack`
    * `RocketChat`
    * `Zulip`
    * `Discord`
    * `Mattermost`
   * An `Angular` Web UI that can be used only to ....?
