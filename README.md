# react-native-ytpl
[![NPM version](https://img.shields.io/npm/v/ytpl.svg?maxAge=3600)](https://www.npmjs.com/package/react-native-ytpl)
[![NPM downloads](https://img.shields.io/npm/dt/ytpl.svg?maxAge=3600)](https://www.npmjs.com/package/react-native-ytpl)
[![Discord](https://img.shields.io/discord/484464227067887645.svg)](https://discord.gg/V3vSCs7)

# this is a fork & port to react native of [TimeForANinja/node-ytpl](https://github.com/TimeForANinja/node-ytpl)

Simple js only package to resolve YouTube Playlists.
Does not require any login or Google-API-Key.

# Support
You can contact us for support on our [chat server](https://discord.gg/V3vSCs7)

# Usage

```js
var ytpl = require('react-native-ytpl');

const playlist = await ytpl('UU_aEa8K-EOJ3D6gOs7HcyNg');
console.log(playlist);
```


# API
### ytpl(id, [options])

Attempts to resolve the given playlist id

* `id`
    * id of the yt-playlist
    * or a playlist url
    * or a user url (resolves to uploaded playlist)
    * or a channel url (resolves to uploaded playlist)
* `options`
    * object with options
    * possible settings:
    * gl[String] -> 2-Digit Code of a Country, defaults to `US` - Allows for localisation of the request
    * hl[String] -> 2-Digit Code for a Language, defaults to `en` - Allows for localisation of the request
    * limit[Number] -> limits the pulled items, defaults to 100, set to Infinity to get the whole playlist - numbers <1 result in the default being used
    * pages[Number] -> limits the pulled pages, pages contain 100 items, set to Infinity to get the whole playlist - numbers <1 result in the default limit being used - overwrites limit
    * requestOptions[Object] -> Additional parameters to passed to [miniget](https://github.com/ShaharBrandman/react-native-ytpl/blob/master/lib/miniget.js), which is used to do the https requests

* returns a Promise
* [Example response](https://github.com/timeforaninja/node-ytpl/blob/master/example/example_output.txt)

### ytpl.continueReq(continuationData)
Continues a previous request by pulling yet another page.  
The previous request had to be done using `pages` limitation.

#### Usage
```js
var ytpl = require('react-native-ytpl');

const playlist = await ytpl('UU_aEa8K-EOJ3D6gOs7HcyNg', { pages: 1 });
console.log(playlist.items);
const r2 = ytpl.continueReq(playlist.continuation);
console.log(r2.items);
const r3 = ytpl.continueReq(r2.continuation);
console.log(r3.items);
```

* returns a Promise resolving into `{ continuation, items }`

### ytpl.validateID(string)

Returns true if able to parse out a (formally) valid playlist ID.

### ytpl.getPlaylistID(string)

Returns a playlist ID from a YouTube URL. Can be called with the playlist ID directly, in which case it just resolves.

* returns a promise resolving into a string containing the id


# Related / Works well with

* [node-ytdl-core](https://github.com/fent/node-ytdl-core)
* [node-ytsr](https://github.com/TimeForANinja/node-ytsr)


# Install

    npm install --save react-native-ytpl


# License
MIT
