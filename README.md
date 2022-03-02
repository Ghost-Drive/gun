
## Quickstart

GUN is *super easy* to get started with:

 - Try the [interactive tutorial](https://gun.eco/docs/Todo-Dapp) in the browser (**5min** ~ average developer).
 - Or `npm install gun` and run the examples with `cd node_modules/gun && npm start` (**5min** ~ average developer).

> **Note:** If you don't have [node](http://nodejs.org/) or [npm](https://www.npmjs.com/), read [this](https://github.com/amark/gun/blob/master/examples/install.sh) first.
> If the `npm` command line didn't work, you may need to `mkdir node_modules` first or use `sudo`.

- An online demo of the examples are available here: http://gunjs.herokuapp.com/
- Or write a quick app: ([try now in a playground](https://jsbin.com/kadobamevo/edit?js,console))
```html
<script src="https://cdn.jsdelivr.net/npm/gun/gun.js"></script>
<script>
// import GUN from 'gun'; // in ESM
// GUN = require('gun'); // in NodeJS
// GUN = require('gun/gun'); // in React
gun = GUN();

gun.get('mark').put({
  name: "Mark",
  email: "mark@gun.eco",
});

gun.get('mark').on((data, key) => {
  console.log("realtime updates:", data);
});

setInterval(() => { gun.get('mark').get('live').put(Math.random()) }, 9);
</script>
```
- Or try something **mind blowing**, like saving circular references to a table of documents! ([play](http://jsbin.com/wefozepume/edit?js,console))
```javascript
cat = {name: "Fluffy", species: "kitty"};
mark = {boss: cat};
cat.slave = mark;

// partial updates merge with existing data!
gun.get('mark').put(mark);

// access the data as if it is a document.
gun.get('mark').get('boss').get('name').once(function(data, key){
  // `once` grabs the data once, no subscriptions.
  console.log("Mark's boss is", data);
});

// traverse a graph of circular references!
gun.get('mark').get('boss').get('slave').once(function(data, key){
  console.log("Mark is the cat's slave!", data);
});

// add both of them to a table!
gun.get('list').set(gun.get('mark').get('boss'));
gun.get('list').set(gun.get('mark'));

// grab each item once from the table, continuously:
gun.get('list').map().once(function(data, key){
  console.log("Item:", data);
});

// live update the table!
gun.get('list').set({type: "cucumber", goal: "jumping cat"});
```

Want to keep building more? **Jump to [THE DOCUMENTATION](#documentation)!**

## Documentation

<table>
  <tr>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/API">API reference</a></h3></td>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/Todo-Dapp">Tutorials</a></h3></td>
    <td style="border: 0;"><h3><a href="https://github.com/amark/gun/tree/master/examples">Examples</a></h3></td>
  </tr>
  <tr>
    <td style="border: 0;"><h3><a href="https://github.com/brysgo/graphql-gun">GraphQL</a></h3></td>
    <td style="border: 0;"><h3><a href="https://github.com/PenguinMan98/electrontest">Electron</a></h3></td>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/React-Native">React & Native</a></h3></td>
  </tr>
  <tr>
    <td style="border: 0;"><h3><a href="https://github.com/sjones6/vue-gun">Vue</a></h3></td>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/Svelte">Svelte</a></h3></td>
    <td style="border: 0;"><h3><a href="https://github.com/Stefdv/gun-ui-lcd#syncing">Webcomponents</a></h3></td>
  </tr>
  <tr>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/CAP-Theorem">CAP Theorem Tradeoffs</a></h3></td>
    <td style="border: 0;"><h3><a href="https://gun.eco/distributed/matters.html">How Data Sync Works</a></h3></td>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/Porting-GUN">How GUN is Built</a></h3></td>
  </tr>
  <tr>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/Auth">Crypto Auth</a></h3></td>
    <td style="border: 0;"><h3><a href="https://github.com/amark/gun/wiki/Awesome-GUN">Modules</a></h3></td>
    <td style="border: 0;"><h3><a href="https://gun.eco/docs/Roadmap">Roadmap</a></h3></td>
  </tr>
</table>

This would not be possible without **community contributors**, big shout out to:

**[ajmeyghani](https://github.com/ajmeyghani) ([Learn GUN Basics with Diagrams](https://medium.com/@ajmeyghani/gundb-a-graph-database-in-javascript-3860a08d873c))**; **[anywhichway](https://github.com/anywhichway) ([Block Storage](https://github.com/anywhichway/gun-block))**; **[beebase](https://github.com/beebase) ([Quasar](https://github.com/beebase/gun-vuex-quasar))**; **[BrockAtkinson](https://github.com/BrockAtkinson) ([brunch config](https://github.com/BrockAtkinson/brunch-gun))**; **[Brysgo](https://github.com/brysgo) ([GraphQL](https://github.com/brysgo/graphql-gun))**; **[d3x0r](https://github.com/d3x0r) ([SQLite](https://github.com/d3x0r/gun-db))**; **[forrestjt](https://github.com/forrestjt) ([file.js](https://github.com/amark/gun/blob/master/lib/file.js))**; **[hillct](https://github.com/hillct) (Docker)**; **[JosePedroDias](https://github.com/josepedrodias) ([graph visualizer](http://acor.sl.pt:9966))**; **[JuniperChicago](https://github.com/JuniperChicago) ([cycle.js bindings](https://github.com/JuniperChicago/cycle-gun))**; **[jveres](https://github.com/jveres) ([todoMVC](https://github.com/jveres/todomvc))**; **[kristianmandrup](https://github.com/kristianmandrup) ([edge](https://github.com/kristianmandrup/gun-edge))**; **[Lightnet](https://github.com/Lightnet)** ([Awesome Vue User Examples](https://glitch.com/edit/#!/jsvuegunui?path=README.md:1:0) & [User Kitchen Sink Playground](https://gdb-auth-vue-node.glitch.me/)); **[lmangani](https://github.com/lmangani) ([Cytoscape Visualizer](https://github.com/lmangani/gun-scape), [Cassandra](https://github.com/lmangani/gun-cassandra), [Fastify](https://github.com/lmangani/fastify-gundb), [LetsEncrypt](https://github.com/lmangani/polyGun-letsencrypt))**; **[mhelander](https://github.com/mhelander) ([SEA](https://github.com/amark/gun/blob/master/sea.js))**; [omarzion](https://github.com/omarzion) ([Sticky Note App](https://github.com/omarzion/stickies)); [PsychoLlama](https://github.com/PsychoLlama) ([LevelDB](https://github.com/PsychoLlama/gun-level)); **[RangerMauve](https://github.com/RangerMauve) ([schema](https://github.com/gundb/gun-schema))**; **[robertheessels](https://github.com/swifty) ([gun-p2p-auth](https://github.com/swifty/gun-p2p-auth))**; **[rogowski](https://github.com/rogowski) (AXE)**; [sbeleidy](https://github.com/sbeleidy); **[sbiaudet](https://github.com/sbiaudet) ([C# Port](https://github.com/sbiaudet/cs-gun))**; **[Sean Matheson](https://github.com/ctrlplusb) ([Observable/RxJS/Most.js bindings](https://github.com/ctrlplusb/gun-most))**; **[Shadyzpop](https://github.com/Shadyzpop) ([React Native example](https://github.com/amark/gun/tree/master/examples/react-native))**; **[sjones6](https://github.com/sjones6) ([Flint](https://github.com/sjones6/gun-flint))**; RIP **[Stefdv](https://github.com/stefdv) (Polymer/web components)**; **[zrrrzzt](https://github.com/zrrrzzt) ([JWT Auth](https://gist.github.com/zrrrzzt/6f88dc3cedee4ee18588236756d2cfce))**; **[xmonader](https://github.com/xmonader) ([Python Port](https://github.com/xmonader/pygundb))**; 

I am missing many others, apologies, will be adding them soon! This list is infintiely old & way out of date, if you want to be listed in it please make a PR! :)

## Testing

You will need to `npm install -g mocha` first. Then in the gun root folder run `npm test`. Tests will trigger persistent writes to the DB, so subsequent runs of the test will fail. You must clear the DB before running the tests again. This can be done by running `rm -rf *data*` command in the project directory.

## Shims

 > These are only needed for NodeJS & React Native, they shim the native Browser WebCrypto API.

If you want to use [SEA](https://gun.eco/docs/SEA) for `User` auth and security, you will need to install:

`npm install @peculiar/webcrypto --save`

Please see [our React Native docs](https://gun.eco/docs/React-Native) for installation instructions!

Then you can require [SEA](https://gun.eco/docs/SEA) without an error:

```javascript
GUN = require('gun/gun');
SEA = require('gun/sea');
```

## Deploy

 > Note: The default examples that get auto-deployed on `npm start` CDN-ify all GUN files, modules, & storage.
 
 > Note: Moving forward, AXE will start to automatically cluster your peer into a shared DHT. You may want to disable this to run an isolated network.
 
 > Note: When deploying a web application using GUN on a cloud provider, you may have to set `CI=false` in your `.env`. This prevents GUN-specific warnings from being treated as errors when deploying your app. You may also resolve this by modifying your webpack config to not try to build the GUN dependencies.

To quickly spin up a GUN relay peer for your development team, utilize [Heroku](http://heroku.com), [Docker](http://docker.com), or any others listed below. Or some variant thereof [Dokku](http://dokku.viewdocs.io/dokku/), K8s, etc. ! Or use all of them so your relays are decentralized too!

### Linux

`SSH` into the home directory of a clean OS install with `sudo` ability. Set any environment variables you need (see below), then do:

```bash
curl -o- https://raw.githubusercontent.com/amark/gun/master/examples/install.sh | bash
```

 > Read [install.sh](https://github.com/amark/gun/blob/master/examples/install.sh) first!
 > If `curl` is not found, *copy&paste* the contents of install.sh into your ssh.

You can now safely `CTRL+A+D` to escape without stopping the peer. To stop everything `killall screen` or `killall node`.

Environment variables may need to be set like `export HTTPS_CERT=~/cert.pem HTTPS_KEY=~/key.pem PORT=443`. You can also look at a sample [nginx](https://gun.eco/docs/nginx) config. For production deployments, you probably will want to use something like `pm2` or better to keep the peer alive after machine reboots.

### [Heroku](https://www.heroku.com/)

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/amark/gun)

 > Heroku deletes your data every 15 minutes, one way to fix this is by adding [cheap storage](https://gun.eco/docs/Using-Amazon-S3-for-Storage).

Or:

```bash
git clone https://github.com/amark/gun.git
cd gun
heroku create
git push -f heroku HEAD:master
```

Then visit the URL in the output of the 'heroku create' step, in a browser. Make sure to set any environment config vars in the settings tab.

### [Zeet.co](https://www.zeet.co/)

[![Deploy](https://deploy.zeet.co/gun.svg)](https://deploy.zeet.co/?url=https://github.com/amark/gun)

Then visit the URL in the output of the 'now --npm' step, in your browser.

### [Docker](https://www.docker.com/)

 > Warning: Docker image is community contributed and may be old with missing security updates, please check version numbers to compare.

[![Docker Automated build](https://img.shields.io/docker/automated/gundb/gun.svg)](https://hub.docker.com/r/gundb/gun/) [![](https://images.microbadger.com/badges/image/gundb/gun.svg)](https://microbadger.com/images/gundb/gun "Get your own image badge on microbadger.com") [![Docker Pulls](https://img.shields.io/docker/pulls/gundb/gun.svg)](https://hub.docker.com/r/gundb/gun/) [![Docker Stars](https://img.shields.io/docker/stars/gundb/gun.svg)](https://hub.docker.com/r/gundb/gun/)

Pull from the [Docker Hub](https://hub.docker.com/r/gundb/gun/) [![](https://images.microbadger.com/badges/commit/gundb/gun.svg)](https://microbadger.com/images/gundb/gun). Or:

```bash
docker run -p 8765:8765 gundb/gun
```

Or build the [Docker](https://docs.docker.com/engine/installation/) image locally:

```bash
git clone https://github.com/amark/gun.git
cd gun
docker build -t myrepo/gundb:v1 .
docker run -p 8765:8765 myrepo/gundb:v1
```

Or, if you prefer your Docker image with metadata labels (Linux/Mac only):

```bash
npm run docker
docker run -p 8765:8765 username/gun:git
```

Then visit [http://localhost:8765](http://localhost:8765) in your browser.

## License

Designed with ♥ by Mark Nadal, the GUN team, and many amazing contributors.

Openly licensed under [Zlib / MIT / Apache 2.0](https://github.com/amark/gun/blob/master/LICENSE.md).

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Famark%2Fgun.svg?size=large)](https://app.fossa.io/projects/git%2Bhttps%3A%2F%2Fgithub.com%2Famark%2Fgun?ref=badge_large)

[YouTube](https://www.youtube.com/channel/UCQAtpf-zi9Pp4__2nToOM8g) . [Twitter](https://twitter.com/marknadal)
