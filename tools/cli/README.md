Table of Content
---
<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
- [Overview](#overview)
  - [Install](#install)
    - [Install with NPM](#install-with-npm)
    - [Build Yourself](#build-yourself)
    - [Both](#both)
  - [Getting Started](#getting-started)
  - [Helpful Links](#helpful-links)
<!-- TOC END -->

# Overview

The CLI tool is currently quite rough, and its main function is to let the Storage Provider Lead perform their duties in a more user-friendly manner than the [extrinsics](https://testnet.joystream.org/#/extrinsics) tab. For this reason, the guide will focus primarily on this side of the tool's functionality.


## Install

There are two ways of installing the CLI.

If you are, or are planning to, run a `storage-node`, build your own node/runtime, or host your own instance of `Pioneer` the CLI is bundled in the [joystream-monorepo](https://github.com/Joystream/joystream). In that case, go [here](#build-yourself). If not, you may have an easier time using the [NPM-package](#install-with-npm).


### Install with NPM
If you have [NPM](https://www.npmjs.com/get-npm) installed:

```
$ npm install -g @joystream/cli
```

### Build Yourself

To get the CLI up and running, on a Mac or Linux based system, you need `yarn`. On Debian based Linux, you will not have much success using `apt`, but you can check out [this guide](/roles/storage-providers/README.md#install-yarn-and-node-on-linux) for help.

```
$ cd ~/
$ git clone https://github.com/Joystream/joystream.git
$ cd joystream
$ yarn install
$ cd cli
$ yarn link
```

### Both
```
# Test that it's working:
$ joystream-cli help
```
Which should return the output below:

```
Command Line Interface for Joystream community and governance activities

VERSION
  @joystream/cli/0.3.0 linux-x64 node-v12.18.

USAGE
  $ joystream-cli [COMMAND]

COMMANDS
  account            Accounts management - create, import or switch currently used account
  api                Inspect the substrate node api, perform lower-level api calls or change the current api provider uri
  autocomplete       display autocomplete installation instructions
  content-directory  Interactions with content directory module - managing classes, schemas, entities and permissions
  council            Council-related information and activities like voting, becoming part of the council etc.
  help               display help for joystream-cli
  media              Higher-level content directory interactions, ie. publishing and curating content
  working-groups     Working group lead and worker actions
```

## Getting Started

The first time you run a command, you will be prompted to set your API-endpoint. This will determine which node you are talking to. If you are running a node locally, you can choose `localhost`. If not, you can connect to the public node, or select a custom endpoint. You can also go the the [api](#api) section to do it manually.

The first time you want to perform an action that requires a key, you will be asked to import one. You can also go the the [account](#account) section to do it manually.

Note that your imports and setting are stored locally at:
- `/home/<Username>/.local/share/joystream-cli` (Linux)
- `c:\Users\<Username>\AppData\Roaming\joystream-cli` (Windows)
- `/Users/<Username>/Library/Application Support/joystream-cli` (Mac OS)

For each command, try `--help` for info on `args` and `options`. For an overview of all `help` outputs, and more info on the CLI, go [here](https://github.com/Joystream/joystream/tree/master/cli).

## Helpful Links

 - For detailed step-by-step guide on how to use `joystream-cli` based on the example of uploading videos using a Windows machine refer to this guide on [medium](https://cyberguy23.medium.com/how-to-upload-videos-to-joystream-from-windows-1dad195956a1) from cyberguy 
 
