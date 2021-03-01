<p align="center"><img src="img/content-creators.svg"></p>

<div align="center">
  <h4>This is a guide for prospective Content Creators on the latest
  <a href="https://testnet.joystream.org/">Joystream Testnet</a>.<h4>
</div>


Table of Contents
==
<!-- TOC START min:1 max:3 link:true asterisk:false update:true -->
- [Overview](#overview)
- [Instructions](#instructions)
  - [Get Started](#get-started)
    - [Create a Channel](#create-a-channel)
    - [Edit a Channel](#edit-a-channel)
    - [Upload a Video](#upload-a-video)
    - [Edit a Video](#edit-a-video)
    - [Content Restrictions](#content-restrictions)
  - [Advanced](#advanced)
    - [Create Channels](#create-channels)
    - [Upload Videos](#upload-videos)
<!-- TOC END -->


# Overview
This page will contain all information on how to act as a `Content Creator`, and how to create a channel, upload videos, and managing your content.

# Instructions
After the Babylon release, content is no longer managed or consumed with [Pioneer](https://testnet.joystream.org). Viewing content is now done in our new consumer app hosted [here](https://play.joystream.org), whereas channel and content management (e.g. registration of channels, uploading, editing, curation, etc.) require the [Joystream-CLI](https://www.npmjs.com/package/@joystream/cli). The CLI can also be built following the instructions [here](/tools/cli/README.md).

## Get Started
If you want to upload content as a `Content Creator`, you need to become a `Member`. Instructions for this can be found [here](https://github.com/Joystream/helpdesk/#get-started).

Once you are a member, you need to fire up your CLI, import your membership key, and connect it to the chain. To get it set up properly, follow the instructions [here](/tools/cli/README.md).

All commands needed for managing content are under the `joystream-cli media` command. This command will show all available subcommands. `joystream-cli media:subCommand --help` will show how to use them.

### Create a Channel
Each member can, by default, create 25 separate channels. If you "need" more, you can ask the `Curator Lead`.
To create one:
```
$ joystream-cli media:createChannel
```
Follow the instructions. Afterwards, your channel will appear in the [UI](https://play.joystream.org), where you can see if your (optional) banner and avatar looks good.

### Edit a Channel
```
$ joystream-cli media:updateChannel
```
Follow the instructions.

### Upload a Video
Each member can, by default, upload a maximum of 100 videos across their channels. If you "need" more, you can ask the `Curator Lead`.
To create one:
```
$ joystream-cli media:uploadVideo /path/to/your/videoFile.ext
```
Follow the instructions. Afterwards, your video will appear in the [UI](https://play.joystream.org), where you can see if your thumbnail looks good.

### Edit a Video
```
$ joystream-cli media:updateVideo
```
Follow the instructions.

### Content Restrictions
It is very important that you do not upload illegal or copyrighted content on our testnets. Firstly, this will result in a disqualification from payouts. It will also result in the takedown of content, potentially slashing of funds, and the deletion of your channel. Multiple spam uploads which represent a burden to moderate for the `Content Curators` may also be penalized and result in deductions on payouts due for qualifying content uploads on your content creator profile.

## Advanced
If you want to create multiple channels, or upload multiple videos in one go, you can pass the information in a JSON file, and use a script to automate the process.

### Create Channels
When you create your first channel:
```
$ joystream-cli media:updateChannel -o /path/to/output.json
```
This will return a valid json that can be used (after modification) as input to create a new channel:

```
$ joystream-cli media:updateChannel -i /path/to/modifiedOutput.json -y
```

The `-y` is optional, in case you are sure it's correct, and doesn't want to confirm your input before sending the extrinsic.

### Upload Videos
The format for the input json:
```
{
  "title": "Title",                                   //required text
  "description": "Description",                       //required text
  "skippableIntroDuration": 0,                        //optional integer - seconds
  "thumbnailUrl": "https://url.to.yourThumbnail.png", //required text - url to thumbnail
  "isPublic": true,                                   //required bool
  "isExplicit": false,                                //required bool
  "hasMarketing": false,                              //required bool
  "publishedBeforeJoystream": 1435104000,             //optional integer - unix timestamp
  "language": {
    "existing": {
      "code": "EN"                                    //required reference - language code
    }
  },
  "category": {
    "existing": {
      "name": "Nonprofits & Activism"                 //required reference - category name
    }
  },
  "license": {
    "new": {
      "knownLicense": {
        "existing": {
          "code": "CC_BY"                             //required reference - license code
        }
      },
      "attribution": "Joystream"                      //some license codes requires attribution to creator
    }
  },
  "media": {
    "new": {
      "encoding": {
        "existing": {
          "name": "H.264_MP4"                         //required reference - license code
        }
      }
    }
  }
}
```
Assuming you saved this file as `/path/to/input.json`, and want to publish to `channel 1` (which you own):

```
joystream-cli media:uploadVideo /path/to/your/videoFile.ext -c 1 -i /path/to/input.json --confirm
```
Combined with a bash script or similar, you can upload all your videos in one go!
