Table of Contents
---
<!-- TOC START min:1 max:4 link:true asterisk:false update:true -->
  - [Examples](#examples)
    - [Channel by ID](#channel-by-id)
    - [Video by ID](#video-by-id)
    - [Videos updated after date/time](#videos-updated-after-datetime)
    - [First videos created](#first-videos-created)
    - [Last videos created](#last-videos-created)
    - [Created before, updated after](#created-before-updated-after)
  - [Arguments](#arguments)
    - [Limits](#limits)
    - [Sorting](#sorting)
    - [Filter](#filter)
<!-- TOC END -->

## Examples
Some useful examples can be found below. Through these examples, alongside the helpers found in the docs, it should be possible to deduce the information required for the role.

### Channel by ID
Some (presumably most) relevant info about a channel with a specific `id`:
```
query {
  channels (where:{id_eq:2 }) {
    id
    createdAt
    updatedAt
    createdInBlock
    title
    category {
      name
    }
    ownerMember {
      id
      handle
      channels {
        id
        title
      }
    }
    coverPhotoAvailability
    avatarPhotoAvailability
    coverPhotoDataObject {
      joystreamContentId
      size
    }
    avatarPhotoDataObject {
      joystreamContentId
      size
    }
    isCensored
    isPublic
  	}
    languages {
      iso
    }
    videos {
      id
      title
      mediaAvailability
      thumbnailPhotoAvailability
    }
}
```

### Video by ID
Some (presumably most) relevant info about a video with a specific `id`:
```
query {
  videos (where:{id_eq:1 }) {
    id
    createdAt
    updatedAt
    updatedById
    deletedAt
    deletedById
    channel {
      id
      title
      ownerMember {
        id
        about
        handle
        controllerAccount
      }
    }
    category {
      id
      name
    }
    title
    description
    duration
    thumbnailPhotoAvailability
    language {
      iso
    }
    hasMarketing
    publishedBeforeJoystream
    isPublic
    isCensored
    isExplicit
    license {
      code
      customText
      attribution
    }
    mediaDataObject {
      joystreamContentId
      size
      liaison {
        workerId
        metadata
      }
    }
    mediaAvailability
    mediaMetadataId
    createdInBlock
    isFeatured
  }
}
```

### Videos updated after date/time
To get videos updated after a certain `timestamp`:
```
query {
  videos (where:{updatedAt_gt:"2021-05-29" }) {
    id
    createdAt
    updatedAt
  }
}
```
```
query {
  videos (where:{updatedAt_gt:"2021-05-29T08:00:00Z" }) {
    id
    createdAt
    updatedAt
  }
}
```

### First videos created
To get first `n` videos created:
```
query {
  videos (limit:10, orderBy:createdInBlock_ASC){
    id
    title
    createdAt
    createdInBlock
  }
}
```
### Last videos created
To get last `n` videos created:
```
query {
  videos (limit:10, orderBy:createdInBlock_DESC){
    id
    title
    createdAt
    createdInBlock
  }
}
```
### Created before, updated after
To get all videos created before some `timestamp`, and updated afters some other `timestamp`
```
query {
  videos (where:{updatedAt_gt:"2021-05-31T08:00:00Z",createdAt_lt:"2021-05-31T07:00:00Z"}) {
    id
    title
    createdAt
    updatedAt
  }
}
```

## Arguments
See examples above for syntax.

### Limits
The default limit is always 50, but this can be modified by adding `(limit: <number>)`.

### Sorting
If you want to order by some specific parameter, click "docs" -> and select the query you are looking for. Then scroll down to `ARGUMENTS`, and click `orderBy` to show the options available in the class.
```
query {
  <yourClass> (orderBy:something_ASC)
}
```

### Filter
Same as above, but click `where`.
```
query {
  <yourClass> (where: {something_eq: "xyz", somethingElse_in: [0-10]})
}
