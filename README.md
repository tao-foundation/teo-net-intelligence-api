TEO Network Intelligence API
============
[![Build Status][travis-image]][travis-url] [![dependency status][dep-image]][dep-url]

This is the backend service which runs along with [rTEO](https://github.com/tao-foundation/rteo) and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to [teo-netstats](https://github.com/tao-foundation/teo-netstats) to feed information.

## Prerequisite

* rTEO
* node
* npm

## Configuration

Configure the app modifying [processes.json](/eth-net-intelligence-api/blob/master/processes.json). Note that you have to modify the backup processes.json file located in `./bin/processes.json` (to allow you to set your env vars without being rewritten when updating).

```js
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // rTEO JSON-RPC host
		"RPC_PORT"        : "8545", // rTEO JSON-RPC port
		"LISTENING_PORT"  : "30303", // rTEO listening port (only used for display)
		"INSTANCE_NAME"   : "teo-node-trustfarm", // whatever you wish to name your node
		"CONTACT_DETAILS" : "trustfarm", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "ws://teostat.tao.foundation:3000", // path to teo-netstats WebSockets api server
		"WS_SECRET"       : "1111", // TEOSTAT server uses passwd for "1111"  WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```

## Run

Run it using pm2:

```bash
cd ~/bin
pm2 start processes.json
```

## Updating

To update the API client use the following command:

```bash
~/bin/www/bin/update.sh
```

It will stop the current netstats client processes, automatically detect your ethereum implementation and version, update it to the latest develop build, update netstats client and reload the processes.

[travis-image]: https://travis-ci.org/cubedro/eth-net-intelligence-api.svg
[travis-url]: https://travis-ci.org/cubedro/eth-net-intelligence-api
[dep-image]: https://david-dm.org/cubedro/eth-net-intelligence-api.svg
[dep-url]: https://david-dm.org/cubedro/eth-net-intelligence-api
