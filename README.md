# `Bourne bot`

Manage (Bourne Identities of) your bots, across Service providers. Based on hashicorp Vault, Secret Hub, and `Kubeseal`.

`Bourne bot`s allows you to manage all your bots, across service providers.

What do I mean by "Service providers" :

- In `CI/CD`'s today's world, there are hundreds of `CI/CD` as a service offers, like `Circle CI`, `travis` ci, `bamboo`, `codeship` (`cloudbees`), `secrethub.io`, `github.com`, `gitlab.com`, `dockerhub`, etc, etc...
- And acutally, what happens, is that we, people, in he `CI/CD`, think of a "robot", a someone, who does all the dirty work for us : it automates tedious, complex operations, to make them reliable, repeatable, and fast.
- Well those robots, int his many-providers contexts, actually use : a `github` user, a `dockerhub` user, a `secrethub` user, a `Circle CI` API Token, etc. etc...
- And now you feel the coming up problem, so let's get to the point :

`Bourne bot` thinks you need an army of bots, instead of one bot per project : it 's like people, they have roles, and there are permissions to do things for some of them, but not for others, etc... That way, if a robot is compromised, then if it gives up all its sedctret, it does not give all permissions on all services of the `CI/CD`.

Plus It's a whole bunch of secrets there, so `Bourne bot` is there to manage this the good way : HashiCorp Vault + Secrethub.

For every bot you create, `Bourne bot` create a bot based on the hubot framework, and creates a github repo for the source code of that bot. Automatically for you, in the github organization of the bot, if it has one (will default to the `Bourne bot` authenticated user's github.com account).

It also gives you one script (one button click _copied-to-clipboard_), to execute in bash session, to open up the project with atom IDE (or your favorite) and the git flow. This script can be derived for a version for every OS distrib of your choice (Mac OS, Windows), or any IDE (VSCode, Atom, eclipse, whatever)

Then you can modify the source code of the bot which already has extras :

- a webhook endpoint to integrate to chatops, etc...
- a prometheus intrumentation endpoint to monitor the bot from `Bourne bot`
- Modify the source code to make the bots have the desired behavior. (about webhooks, may also expose REST API)
- bpmn on some day to implement security policies as defined per organization Security Officer ?

# References

- Something open source from hashicorp :
  - https://www.hashicorp.com/blog/vault-aide-a-chatops-bot-for-hashicorp-vault
  - https://github.com/DigitalOnUs/VaultAIDE
- how many open source project exists on the topic ?
  - (not much, or say none at all) : https://github.com/search?q=hashicorp+vault+bot&type=repositories
  - only one worth mentioning [a repo](https://github.com/ezafeire/sensitive-data-leak-prevention) whose idea was to (also note that this bot was made with probot like one of th [top rated discord bots rated top.gg](https://top.gg) ) :

> A `probot` application that automatically detects and deletes github issues that contain sensitive data such as Hashicorp Vault tokens and role-id's. The bot will asynchronously detect posts, delete them, re-create them with the sensitive data redacted and inform the user of the deletion.

- Can the `hubot` framework work with :
  - [x] [`Slack`](#) https://github.com/slackapi/hubot-slack
  - [x] [`Discord`](#) https://github.com/thetimpanist/hubot-discord
  - [x] [`RocketChat`](https://github.com/RocketChat/Rocket.Chat)
  - [x] [`Zulip`](https://github.com/zulip/zulip) https://github.com/zulip/hubot-zulip

## Git based, hugo?

See https://github.com/pokusio/pokusbot-hugo-theme as a hugo theme that can be used for many purposes

# Design

The bot needs to be able to :

- `C.R.U.D.` `Hashicorp Vault` secrets
- `C.R.U.D.` `secrethub` secrets
- `C.R.U.D.` `Kubeseal` secrets
- `C.R.U.D.` the Mongo database of all identities
-
- prometheus exporter for both the bot and the REST API
- architecture :
  - a REST API to implement all vaults' standard ops (`C.R.U.D.`) in `Loopback 4`
  - a bot (which can be scaled) to run all REST API standard ops (`C.R.U.D.`) from (one bot for each chatops) :
    - `Slack`
    - `RocketChat`
    - `Zulip`
    - `Discord`
    - `Mattermost`
  - An `Angular` Web UI that can be used only to ....?
- Use https://github.com/pokusio/pokusbot-hugo-theme as a hugo theme, to make one commit for every operation on each secret's activity :
  - the bot will make a new hugo post of type of one specific bot, to log a "commit message" for every operation on the secret :
    - that's what i missed about secret hub, to have commit messages for each secret operation, since every operation brings a new secret version /
    - and there instead of a simple commit message, i have a full hugo page, a content entry which is a much more structured dataset unit
    - I want to also generate stats graphs
