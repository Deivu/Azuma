# Azuma
A package that actually syncs your ratelimits across all your clusters on Discord.JS

> The Shipgirl Project; [Azuma](https://azurlane.koumakan.jp/Azuma)

<p align="center">
  <img src="https://azurlane.netojuu.com/w/images/4/42/Azuma.png">
</p>

## EOL 
> Discord.JS started developing their "proxy" module, marking the end of EOL of this package. Use that instead

> Link: https://github.com/discordjs/discord.js/tree/main/packages/proxy

## Features

✅ An easy drop in solution for those who wants globally synced ratelimits

✅ Follows the original Discord.JS rest manager, so no breaking changes needed

✅ Supports Discord.JS v13


## NOTE

> This library is now in "Maintenance" phase. I'm not gonna add new features on it. I'll just fix issues if there is but that's as far as I'll go.

> You need to use [Kurasuta](https://github.com/DevYukine/Kurasuta) to make this work as this package depends on it

> This is planned to use `@discordjs/sharder` once it's ready. That's the last update and marks the v4 release

> v1.x.x initial release (Latest in 1x branch is version: 1.1.0)

> v2.x.x drops support for Discord.JS v12 (Latest in 2x branch is version: 2.1.2)

> v3.x.x makes the package ESM only (Current)

## Installation

> npm i --save azuma

## Documentation

> https://deivu.github.io/Azuma/?api

## Support
> https://discord.gg/FVqbtGu `#development` channel

## Example
> Running Azuma is the same with [Kurasuta](https://github.com/DevYukine/Kurasuta#example), except on you need to change your index.js based on example below

## Example of index.js
```js
import { Azuma } from 'azuma';
import { Client } = from 'discord.js';

const KurasutaOptions = {
    client: YourBotClient,
    timeout: 90000,
    token: 'idk'
};
const AzumaOptions = {
    inactiveTimeout: 300000,
    requestOffset: 500
};
// Initialize Azuma
const azuma = new Azuma(new URL('BaseCluster.js', import.meta.url), KurasutaOptions, AzumaOptions);
// If you need to access the Kurasuta Sharding Manager, example, you want to listen to shard ready event
azuma.manager.on('shardReady', id => console.log(`Shard ${id} is now ready`));
// Call spawn from azuma, not from kurasuta
azuma.spawn();
```

## Pro Tip
> Azuma also exposes when a request was made, when a response from a request is received, and if you hit an actual 429 via an event emitter, which you can use to make metrics on
```js
import { Client } = from 'discord.js';

class Example extends Client {
  login() {
    this.rest.on('onRequest', ({ request }) => /* do some parses on your thing for metrics or log it idk */);
    this.rest.on('onResponse', ({ request, response }) => /* do some parses on your thing for metrics or log it idk */);
    this.rest.on('onTooManyRequest', ({ request, response }) => /* do some probably, warning logs here? since this is an actual 429 and can get you banned for an hour */);
    return super.login('token');
  }
}
```
> WARNING: DO NOT CHANGE OR RUN ANY FUNCTION FROM THE PARAMETERS. It's designed to be used as read-only values

> Based from my old handling from `@Kashima`, Made with ❤ by @Sāya#0113
