# Source: https://docs.samply.app/api/players.html

# Players (Links) [​](https://docs.samply.app/#players-links)

Players (also known as Links) are shareable windows into your [projects](https://docs.samply.app/./projects.html). Each player defines which files are accessible and listener permissions. Players can be public or restricted via passwords, paywalls, or limited to invited collaborators.

Note

In the Samply API, you’ll see the term “Player,” but in the app, these are just called “Links.” They’re effectively the same thing. So if you want to create or manage links via the API, you'll be working with players.

## Create a player [​](https://docs.samply.app/#create-a-player)

This endpoint creates a player and returns a [player object](https://docs.samply.app/./players.html#player-object).

Request type `POST`

Endpoint `/players`

### Attributes [​](https://docs.samply.app/#attributes)

js

```
{
  name: string,
  projectid: string,
  folderid: string,
  boxids: string[],
  public: boolean,
  upload: {
    enabled: boolean,
    header: string,
    greeting: string,
    redirect: string
  },
  options: {
    quality: "original" | "compressed" | "lossless",
    metadata: boolean,
    isrc: boolean,
    downloads: boolean,
    comments: boolean,
    loudnessMatch: boolean,
    targetLufs: number,
    loudnessPlatform: "amazon-music" | "apple-music" | "deezer" | "spotify" | "tidal" | "youtube"
    studio: boolean,
    stacks: boolean,
    samplyCTA: boolean,
    boxSubtitle: "artist" | "timestamp" | "none",
  },
  payment: {
  	price: number;
  	fulfillment: "allow-download" | "allow-access",
  	recipient: "everyone" | "customer"
  },
  collaborators: [
    {
      email: string,
      role: "admin" || "editor" || "viewer"
    }
  ],
  sortBy: {
    criterion: "custom" || "name" || "duration" || "size" || "bitDepth" || "sampleRate" || "bitRate" || "channels" || "lufs" || "timeModified" || "timeCreated" || "kind",
    ascending: boolean
  }
}
```

---

#### name string

Human readable title of player.

---

#### projectid string optional

Creates a player for an existing project without creating a new project.

---

#### folderid string optional

The id of the folder within a project for which a player will be created. If this field is provided, the projectid of the containing project must be provided as well.

---

#### boxids string array optional

The ids of all boxes within a project to include in a created player. If this field is provided, the projectid of the containing project must be provided as well. If this field is provided, folderid must not be provided.

---

#### public boolean optional

Whether player link is public. If no value is provided, the player will fallback to the creator's player preference set in-app ('Anyone with the link' corresponds to public = true and 'Collaborators only' corresponds to public = false). If the creator has no default player preference set, this value will fall back to true.

---

#### upload object optional

Public upload link options.

###### Child attributes

---

#### enabled boolean optional

Enable upload portal.

---

#### header string optional

Upload portal title.

---

#### greeting string optional

Upload portal subheader.

---

#### redirect string optional

Link to redirect user after upload has completed.

---

#### options object optional

Player configuration options.

###### Child attributes

---

#### quality 'original' | 'compressed' | 'lossless' optional

Default audio playback quality. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will remain undefined. If undefined, the frontend implementation will attempt to playback the player at the highest quality that the listener's internet connection will allow.

---

#### metadata boolean optional

Whether to show metadata in player if uploaded files include metadata. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be false.

---

#### isrc boolean optional

Whether to show isrc codes in player if uploaded files include them. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be false.

---

#### downloads boolean optional

Whether to allow downloads. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be true.

---

#### comments boolean optional

Whether to allow commenting. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be true.

---

#### loudnessMatch boolean optional

Whether to enable loudness matching. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be false.

---

#### targetLufs boolean optional

Target LUFS value if loudness matching is enabled. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be undefined.

---

#### loudnessPlatform boolean optional

Target loudness platform LUFS value if loudness matching is enabled. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be undefined.

---

#### studio boolean optional

Enable studio branding if creator has configured it. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be false.

---

#### stacks boolean optional

Enable all versions in the player. If this value is true, all versions will be available to the listener. If false, only the most recent versions are available. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be false.

---

#### boxSubtitle 'artist' | 'timestamp' | 'none' optional

Which value to show below each track in a player. By default, this value is set to artist. The artist will be the metadata artist provided on the file. If no artist metadata is present, this value will fall back to the file uploader.

---

#### samplyCTA boolean

Whether to show Samply post-download popup after user downloads files from a player. If no value is provided, this value will fall back to the creator's default player preference. If no default player preference is found, this value will be true.

---

#### payment object optional

Paywall configuration. Your Stripe payments integration must be set up before setting this attribute.

###### Child attributes

---

#### price number

The paywall price in cents.

---

#### fulfillment 'allow-download' | 'allow-access'

The action that will be enabled after a listener has paid for the player. Allow-download will enable downloads. Allow-access will enable viewing access.

---

#### recipient 'everyone' | 'customer'

Who gains access when a user pays. When set to 'everyone', all users gain access after one user pays. When set to 'customer' only the paying user gains access after paying.

---

#### collaborators collaborator array optional

An array of collaborator objects.

---

#### collaborator object optional

The email and permissions for a single collaborator on a project.

###### Child attributes

---

#### email string

User email address.

---

#### role 'admin' | 'editor' | 'viewer'

User permission on a player.

---

#### sortBy object optional

File sort options if creating a project.

###### Child attributes

---

#### criterion 'custom' | 'name' | 'duration' | 'size' | 'bitDepth' | 'sampleRate' | 'bitRate' | 'channels' | 'lufs' | 'timeModified' | 'timeCreated' | 'kind' optional

Sort criterion for project files.

---

#### ascending boolean optional

Whether to sort in ascending order.

## Update a player [​](https://docs.samply.app/#update-a-player)

This endpoint updates an existing player and returns a [player object](https://docs.samply.app/./players.html#player-object).

Request type `POST`

Endpoint `/players/:playerid`

js

```
{
  name: string,
  public: boolean,
  options: {
    quality: "original" | "compressed" | "lossless",
    metadata: boolean,
    isrc: boolean,
    downloads: boolean,
    comments: boolean,
    loudnessMatch: boolean,
    targetLufs: number,
    loudnessPlatform: "amazon-music" | "apple-music" | "deezer" | "spotify" | "tidal" | "youtube",
    studio: boolean,
    stacks: boolean,
    samplyCTA: boolean,
  },
  payment: {
    price: number;
    fulfillment: "allow-download" | "allow-access",
    recipient: "everyone" | "customer"
  }
}
```

---

#### name string optional

Human readable title of player.

---

#### public boolean optional

Whether player link is public.

---

#### options object optional

Player configuration options.

###### Child attributes

---

#### quality 'original' | 'compressed' | 'lossless' optional

Default audio playback quality.

---

#### metadata boolean optional

Whether to show metadata in player if uploaded files include metadata.

---

#### isrc boolean optional

Whether to show isrc codes in player if uploaded files include them.

---

#### downloads boolean optional

Whether to allow downloads.

---

#### comments boolean optional

Whether to allow commenting.

---

#### loudnessMatch boolean optional

Whether to enable loudness matching.

---

#### targetLufs boolean optional

Target LUFS value if loudness matching is enabled.

---

#### loudnessPlatform boolean optional

Target loudness platform LUFS value if loudness matching is enabled.

---

#### studio boolean optional

Enable studio branding if creator has configured it.

---

#### stacks boolean optional

Enable all versions in the player. If this value is true, all versions will be available to the listener. If false, only the most recent versions are available.

---

#### samplyCTA boolean

Whether to show Samply post-download popup after user downloads files from a player.

---

#### payment object optional

Paywall configuration. Your Stripe payments integration must be set up before setting this attribute.

###### Child attributes

---

#### price number

The paywall price in cents.

---

#### fulfillment 'allow-download' | 'allow-access'

The action that will be enabled after a listener has paid for the player. Allow-download will enable downloads. Allow-access will enable viewing access.

---

#### recipient 'everyone' | 'customer'

Who gains access when a user pays. When set to 'everyone', all users gain access after one user pays. When set to 'customer' only the paying user gains access after paying.

## Get a player [​](https://docs.samply.app/#get-a-player)

This endpoint returns a [player object](https://docs.samply.app/./players.html#player-object) by id.

Request type `GET`

Endpoint `/players/:playerid`

## List owned players [​](https://docs.samply.app/#list-owned-players)

This endpoint returns an array of all [player objects](https://docs.samply.app/./players.html#player-object) the caller owns.

Request type `GET`

Endpoint `/players`

## Player object [​](https://docs.samply.app/#player-object)

All player actions will return a player object with the following structure.

js

```
{
  name: string,
  id: string,
  projectid: string,
  folderid: string,
  boxids: string[],
  color: string,
  object: 'player',
  public: boolean,
  timeCreated: number,
  timeModified: number,
  options: {
    quality: "original" | "compressed" | "lossless",
    metadata: boolean,
    isrc: boolean,
    downloads: boolean,
    comments: boolean,
    loudnessMatch: boolean,
    targetLufs: number,
    loudnessPlatform: "amazon-music" | "apple-music" | "deezer" | "spotify" | "tidal" | "youtube",
    studio: boolean,
    stacks: boolean,
    samplyCTA: boolean,
    boxSubtitle: "artist" | "timestamp" | "none",
  }
}
```

---

#### name string readonly

Human readable title of player.

---

#### id string readonly

Player id.

---

#### projectid string readonly

Project id.

---

#### folderid string readonly optional

Folder id. This parameter is present if the player is scoped to a folder.

---

#### boxids string array readonly optional

Array of boxids contained in the player. This parameter is present if the player is scoped to specific boxids.

---

#### color string readonly

Player color in hex format.

---

#### object player readonly

Object type of returned object.

---

#### public boolean readonly

Whether player link is public.

---

#### timeCreated number readonly

Time created in millis since Unix epoch.

---

#### timeModified number readonly

Time modified in millis since Unix epoch.

---

#### options object readonly

Player configuration options.

###### Child attributes

---

#### quality 'original' | 'compressed' | 'lossless' readonly

Default audio playback quality.

---

#### metadata boolean readonly

Whether to show metadata in player if uploaded files include metadata.

---

#### isrc boolean readonly

Whether to show isrc codes in player if uploaded files include them.

---

#### downloads boolean readonly

Whether to allow downloads.

---

#### comments boolean readonly

Whether to allow commenting.

---

#### loudnessMatch boolean readonly

Whether to enable loudness matching.

---

#### targetLufs boolean readonly

Target LUFS value if loudness matching is enabled.

---

#### loudnessPlatform boolean readonly

Target loudness platform LUFS value if loudness matching is enabled.

---

#### studio boolean readonly

Enable studio branding if creator has configured it.

---

#### stacks boolean readonly

Enable all versions in the player. If this value is true, all versions will be available to the listener. If false, only the most recent versions are available.

---

#### samplyCTA boolean readonly

Whether to show Samply post-download popup after user downloads files from a player.