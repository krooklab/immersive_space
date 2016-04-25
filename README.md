# midi2iosono: control Barco IOSONO using MIDI signals

## Installing midi2iosono

To install, please make sure [NodeJS](https://nodejs.org/en/) >= 4.0.0 and optionally (git)[https://git-scm.com/] are installed.
Run the following commands in bash:

```bash
git clone https://github.com/krooklab/midi2iosono.git
# or wget https://github.com/krooklab/midi2iosono/archive/master.zip; unzip master.zip
cd midi2iosono
npm install
```

## Configuring midi2iosono

Before running *midi2iosono*, a configuration JSON file needs to be prepared.

### IOSONO parameters

| parameter         | type      | description | default |
|-------------------|-----------|-------------|---------|
| `measurements`    | `Object`  | An object containing the measurements of the IOSONO speaker setup, specified for each axis. Each value is specified in meters. | `{ "x": 10, "y": 10, "z": 10 }` |
| `bundled`         | `boolean` | When `true`, all channel positions are send a OSC bundle. | `false`|
| `channels`         | `Number` | The number of channels to send to iosono, starting from 0. | `16`|
| `host`         | `String` | The IP address of the IOSONO. | `192.168.0.1`|
| `port`         | `String` | The port of the IOSONO. | `4001`|
| `localAddress`         | `String` | The IP address to send OSC messages from. | `0.0.0.0`|
| `localPort`         | `String` | The port to send OSC messages from. | `5001`|

### MIDI parameters

| parameter         | type      | description | default |
|-------------------|-----------|-------------|---------|



A complete example is given below.

```JSON
{
    "iosono": {
        "measurements": {
            "x": 10,
            "y": 10,
            "z": 10
        },
        "bundled": false,
        "channels": 1,
        "host": "192.168.0.1",
        "port": 3333,
        "localAddress": "0.0.0.0",
        "localPort": 2222,
        "address": "example.org/iosono"
    },
    "midi": {
        "name": "MIDI-2-IOSONO",
        "mapping": {
            "noteOn": {
                "key": {
                    "x": [24, 35]
                },
                "velocity": {
                    "y": [0, 100]
                }
            },
            "pitchBend": {
                "bend": {
                    "z": [0, 100]
                }
            }
        }
    }
}
```

## Running midi2iosono

You can simply run *midi2iosono* in bash.

`./midi2iosono [config.json]`

The config file can be supplied as a command line parameter or put as `config.json` in the working directory.
