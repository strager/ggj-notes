# GGJ notes

Programming notes in preparation for Global Game Jam 2015.

## Make

    .DELETE_ON_ERROR:

    node_modules/.stamp: package.json
            npm install
            touch $@

## Phaser

Get the source:

    cp phaser/typescript/*.d.ts phaser/build/phaser.* project/phaser/

TypeScript:

    /// <reference path="../phaser/phaser.d.ts" />

Snippets:

    var upKey: Phaser.Key = game.input.keyboard.addKey(Phaser.Keyboard.UP);
    game.stage.disableVisibilityChange = true;
    game.time.desiredFps = 30;

## TypeScript

Setup:

    npm install tsc  # Or should we use package.json?

Run the compiler:

    tsc --out src/client.js src/client.ts src/shared.ts
    tsc --module commonjs --out src/server.js src/server.ts src/shared.ts

## ProtoBuf.js

In `package.json`:

    "dependencies": {"protobufjs": "3.8.2"}

Compile:

    node_modules/protobufjs/bin/proto2js src/protocol.proto -commonjs > src/protocol.server.js
    node src/protocol.server.js  # Check for errors.
    node_modules/protobufjs/bin/proto2js src/protocol.proto -class > src/protocol.client.js

## Live reload

(This kinda sucks right now.)

    supervisor -w src/server.js src/protocol.server.js -- src/server.js
