<h1 align="center">
  <br>
  <a href="http://ferment.audio"><img src="/ferment-logo.png" alt="WebTorrent" width="200"></a>
  <br>
  Ferment
  <br>
  <br>
</h1>

[Ferment](http://ferment.audio) is a peer-to-peer audio publishing and streaming application. It is an attempted re-creation of classic SoundCloud, but runs entirely decentralized instead of one corporation and its investors holding all the power. 💞 🍻

It is made possible by combining these **amazing** projects: [ssb](https://scuttlebot.io/), [webtorrent](https://webtorrent.io/) and [electron](http://electron.atom.io/).

[📺 Watch a quick video demo](https://www.youtube.com/watch?v=xgvxXbWYmrI)

[🔽 Download for macOS](https://github.com/mmckegg/ferment/releases)

[🛠 Build from source](#install)

[💖 Donate and support me on Patreon](https://www.patreon.com/MattMcKegg)

<img src="/assets/ferment-screenshot-0.0.0.jpg" alt="WebTorrent" width="888" height="688" />

## Experimental // EVERYTHING IS SUBJECT TO CHANGE AND BREAKING!

I'm just fiddling with ideas right now. My goal is to replace my need for SoundCloud as a [backyard musician that uploads WAY to much stuff](https://soundcloud.com/destroy-with-science). I no longer want to pay them $200 a year to host it all (also sick of being told to pay more money to get SoundCloud Go and having my feed ransomed out from underneath me).

### The long-term vision ✨

I want to see a thriving audio sharing community (actually would be COMMUNITIES! it's decentralized), a lot like SoundCloud used to encourage before it had to MONETIZE and start trying to make a profit (AND OH NOEZ, WE'RE GOING BANKRUPT 😞). Pretty sure that SoundCloud was doomed from the start (so glad we had all these great years off the pocket of those investors), but a _peer-to-peer decentralized not-for-profit open source_ might just work!

**It will also soon be possible to host your own server that allows people without the app to stream music from your profile (or others that you want to seed).** This will still be peer-to-peer but your server will act as a mirror and tracker.

## How it works

Ferment uses a peer-to-peer gossip protocol called [Secure Scuttlebutt](https://scuttlebot.io/more/protocols/secure-scuttlebutt.html). The best part about this is there is no central server and no single point of failure. In fact everyone on the network is a server, with a copy of all of their friends and their friend's friends data. You gossip with other peers to find out if any of your shared contacts have any new posts and share them. But by gossip, we mean cryptographically prove everything they've said since the last time you heard from them. It is impossible to skip a message.

[Finding peers across the complex topography of the internet is pretty difficult though](https://scuttlebot.io/more/articles/design-challenge-avoid-centralization-and-singletons.html). This is where pub servers come in. They act as gossip hubs where information can be shared across networks. A pub is just an ordinary Ferment peer that has a publicly accessible IP address and can be remotely connected to on demand.

The actual audio files are just torrents (a special variant called [webtorrent](https://github.com/feross/webtorrent) that works over WebRTC). The SSB message contains a reference to its magnet url, and you seed the file to other ferment peers.

Whenever you listen to something in Ferment, you start seeding that file with other peers. It will be cached on your machine until you remove it (right-click > Stop Sharing Post). In the future this will be handled automatically (you'll only cache material you have "liked" and selected content from followed users that are weak on the network).

## Ferment and Copyright

Ferment is an audio publishing platform for **copyright-owning creators** and **creative commons licensed material**. As this is a decentralized, peer-to-peer community, what you culture in your network is up to you. **You get to choose what level of sharing legality you are comfortable with.**

For example, if someone in your network adds copyrighted material, and you listen to it, your Ferment will start sharing the file. If you don't want to share the legal responsibility for this, right-click and select 'Stop Sharing Post.'

You could also consider unfollowing them and reporting the infringement to the owner of the pub to prevent the spread of the material.

**A pub owner should unfollow anyone who adds material which infringes copyright.**

## Requirements

If there is no [packaged app](https://github.com/mmckegg/ferment/releases) for your platform, you'll need to build from source using modern version of [`node` and `npm`](https://nodejs.org).

## Install

### on macOS

Download the latest release [here](https://github.com/mmckegg/ferment/releases)!

**Make sure you read the section of this readme titled ["Joining Pub Server"](#joining-pub-server)!**

### from npm

```bash
$ npm install -g ferment
```

And then run using:

```bash
$ ferment
```

If you get an error appear saying something like [`Module version mismatch. Expected 50, got 48.`](https://github.com/mmckegg/ferment/issues/5), try running the following:

```bash
# requires automake on your system
$ ferment --rebuild
```

Install latest updates:

```bash
$ npm install -g ferment@latest && ferment --rebuild
```

If you get weird issues, trash it and reinstall:

```bash
$ npm rm -g ferment
```


### from source

**Warning:** Development is done on the master branch, so this could be broken right now!

```bash
$ git clone https://github.com/mmckegg/ferment.git
$ cd ferment
$ npm install
```

And then run using:

```bash
$ npm start
```

Install latest updates:

```bash
$ npm update
$ npm run rebuild # make sure native add-ons are compatible with electron version
```

If you get weird issues, trash your `ferment/node_modules` directory:

```bash
$ rm -rf node_modules
$ npm install
```

## Joining Pub Server

By default, **Ferment** will only see other users that are on the same local area network as you. In order to share with users on the internet, you need to be invited to a pub server.

Since I'm a nice person 💖 you can hang out in my pub, and you don't even have to buy any drinks! 🍻 But please be mindful about uploading content that you do not own the rights to. My pub will [unfollow anyone who uploads content that I don't think is _fair_ to the original creators](#ferment-and-copyright).

**Click 'Join Pub' on the sidebar then paste the code below:**

```
pub.ferment.audio:43761:@uIL3USK7QJg5AHohnZC329+RXS09nwjc24ulFBH2Ngg=.ed25519~MqAyQji/+ZHHtq9JM8Dl/w6hOujxXAxlOpYiFUfLgRM=
```

> **NOTE:** To avoid destroying my server, this code can only be used a limited amount of times. Please post an issue if it doesn't work for you, and I'll generate a new one.

If all goes to well, you'll start to see audio appear before your eyes! Give that play button a spin.

However, if you don't see anything appear after about 30 seconds, try restarting ferment. It may take a minute or two before it appears. You should be all good as long as `+connected pub.ferment.audio:43761:....` appears in your terminal.

**If you receive an error message, it probably means my pub server has locked up. This seems to be happening a bit at the moment, [trying to get to the bottom of it](https://github.com/mmckegg/ferment/issues/7).** Let me know and I'll restart it. In the mean time, you could start creating a shiny profile and adding some tunes!

## Hosting Your Own Pub Server

See [this guide](http://ssbc.github.io/docs/scuttlebot/howto-setup-a-pub.html) for full info setting up [scuttlebot](http://ssbc.github.io/scuttlebot/).

### Ferment flavoured pub server

Ferment includes it's own bundled server app that you can run which also functions as a tracker and torrent seeder. It also scopes the network, only replicating ferment feeds with you (rather than the normal 3-hop friend replicate, which gives you a bunch of other ssb data, which you won't be able to see but takes up hard-drive space and makes things slow for no reason).

This is all super undocumented now. Eventually there will be a one-click style install. Or at least some step by step instructions for different platforms.

Here's a hint to get started:

```
xvfb-run npm run server -- --host={yourhostname} --seed {YOUR_ID}
```

## TODO

- [x] Scuttlebot database
- [x] Webtorrent streaming
- [x] Layout main application interface, base styles
- [x] Audio player interface
- [x] Sequencial feed playback
- [x] API for adding file (transcode, analyse waveform)
- [x] Upload interface [still needs more fields, and artwork]
- [x] Connect to local peers and merge streams
- [x] Store artwork in blobstore, and retrieve again
- [x] User setup (choose display name, bio, picture)
- [x] Specific Artist Feed
- [x] Proper play/pause/loading buttons (nice try emoji)
- [x] Follow other users ("friends")
- [x] Display following stats
- [x] Likes
- [x] Backgrounding (keep seeding / syncing when main window is closed)
- [x] Invite to pub
- [x] Make torrents more reliable via pub server trackers [still need to make this work for other pubs though, hard coded to pub.ferment.audio right now]
- [x] Allow revisions (some kind of special reply that replaces the content with new content)
- [x] Show seed stats
- [x] Reposting
- [x] Make Save / Download buttons work
- [x] Automatically download/seed items from people you follow
- [ ] Allow "delete" of audio posts (some kind of tombstoning)
- [ ] Playlists
- [ ] Commenting (time based)

### Server

- [x] Pub server (invites, etc)
- [x] Seed torrents from specified feeds
- [ ] Web interface for viewing specified feeds (started in [branch](https://github.com/mmckegg/ferment/tree/web-lite-client))

## License

GPL-3.0
