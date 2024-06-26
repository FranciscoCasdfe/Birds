<img src="static/apple-touch-icon.png" align="right" />

# Board Games in 3D!

This is a board game engine created in Three.js and Rust, designed to make it as easy as possible to start playing a boardgame online.


## Building

Building is simple. You will need a recent version of Rust + NPM.

First, install the npm packages with `npm install`. Next, run `build.sh`. You're done!
(Right now I'm patching Three.js to only export `/src/Three.js`, for better tree-shaking).

## Usage


**Controls:**
- <kbd>Left click</kbd> and drag to orbit
- <kbd>Shift click</kbd> and drag to pan
- <kbd>Scroll wheel</kbd> to zoom
- <kbd>Click and drag</kbd> to move objects
- <kbd>T</kbd> to take an object or card from a bag or deck
- <kbd>G</kbd> to add a card to your hand
- And of course <kbd>Right click</kbd> any object for more!

## Making games

Creating a new game is easy. Just zip up your assets with a `manifest.json` along with a script like `game.js`.
Then just drag your zip file onto the game window.

You can register up to 40MiB of assets (each under 2 MiB), which will be stored and distributed on the server
until the lobby closes.

**Warning**: Your game code runs in a web worker, which means that any state or logic can't be transferred.
If the host leaves, all other users will be kicked out to prevent broken games.
If you don't want this to happen, call `self.world.close()` to indicate that your plugin is done.

There isn't any documentation yet, but take a look at `static/js/prelude.js` and `plugins/*/` for guidance.

For models:
- Add colliders to GLTF files by adding a custom `collider` property set to either `box` or `cylinder`.
- Units are in inches.
