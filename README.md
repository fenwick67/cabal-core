# cabal-node

Node.js library for p2p functions for chat.

## Usage

    npm install cabal-node

## API

> var Cabal = require('cabal-node')

### var cabal = Cabal([storage][, key][, opts])

Create a cabal p2p database using storage `storage`, which must be either a
string (filepath to directory on disk) or an instance of
[random-access-storage](https://github.com/random-access-storage/).

If this is a new database, `key` can be omitted and will be generated.

### cabal.getChannels(cb)

Retrieve a list of all channel names that exist in this cabal.

### var rs = cabal.readMessages(channel, opts)

Returns a readable stream of messages (most recent first) from a channel.

Pass `opts.limit` to set a maximum number of messages to read.

### cabal.listenMessages(channel, fn)

Calls `fn` with every new message that arrives from this point onwards.

### cabal.publish(message, opts, cb)

Publish `message` to your feed. `message` must have a `type` field set. If not,
it defaults to `chat/text`. In general, a message is formatted as

```js
{
  type: 'text/chat',
  content: {
    text: 'hello world',
    channel: 'cabal-dev'
  }
}
```

A `timestamp` field is set automatically with the current system time.

`type` is an unrestricted field: you can make up new message types and clients
will happily ignore them until someone implements support for them. Well
documented types include

#### chat/text

```js
{
  type: 'chat/text',
  content: {
    text: 'whatever the user wants to say',
    channel: 'some channel name. if it didnt exist before, it does now!'
  }
}
```

### var ds = cabal.replicate()

Creates a new, live replication stream. This duplex stream can be piped into any
transport expressed as a node stream (tcp, websockets, udp, utp, etc).

## License

AGPLv3
