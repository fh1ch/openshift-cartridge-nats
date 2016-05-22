NATS cartridge for OpenShift
============================

This is a custom OpenShift cartridge for [NATS](http://nats.io/), a open-source,
high-performance, lightweight cloud native messaging system

## Usage

### Using [web console](https://openshift.redhat.com/app/console/applications)

Open your application in the [web console](https://openshift.redhat.com/app/console/applications),
go to **"See the list of cartridges you can add"**, paste the URL below in
**"Install your own cartridge"** textbox at the bottom of the page and click
"Next".

```
https://raw.githubusercontent.com/fh1ch/openshift-cartridge-nats/master/metadata/manifest.yml
```

Then you can use `NATS_URL` environment variable to connect from an
application running in the main web cartridge.

For instance, here's how you'd do it in a Node.js application using
[node-nats](https://github.com/nats-io/node-nats):

```js
var nats = require('nats');
...
var nc = nats.connect({
  url: process.env.NATS_URL
});
```

### Using the command line

Make sure you have `rhc` installed (see [here](https://developers.openshift.com/en/managing-client-tools.html)).

If you want to **add** a NATS instance based on this cartridge to an existing
application:

```sh
rhc cartridge-add https://raw.githubusercontent.com/fh1ch/openshift-cartridge-nats/master/metadata/manifest.yml \
  --app appname
```

...where `appname` is the name of your application.

To **create** an app based on the standard Node.js v0.10 cartridge and this one,
run:

```sh
rhc app create appname \
  nodejs-0.10 \
  https://raw.githubusercontent.com/fh1ch/openshift-cartridge-nats/master/metadata/manifest.yml
```

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2016 Fabio Huser <fabio@fh1.ch>
