# Factorio Server Docker [![Docker Stars](https://img.shields.io/docker/stars/deniszholob/factorio-server-docker.svg)](https://hub.docker.com/r/deniszholob/factorio-server-docker/) [![Docker Stars](https://img.shields.io/docker/stars/deniszholob/factorio-server-docker.svg)](https://hub.docker.com/r/deniszholob/factorio-server-docker/)
Docker for a [factorio](https://www.factorio.com/) server

# Usage

```
docker run -d -p 34197:34197/udp \
  -v /factorio:/opt/factorio \
  --name factorio \
  --restart=always  \
  deniszholob/factorio-server-docker
```
What does it mean?

* `-d` - Run as a daemon ("detached").
* `-p` - Expose ports.
* `-v` - Mount `/factorio` on the local file system to `/opt/factorio` in the container.
* `--restart` - Restart the server if it crashes and at system start
* `--name` - Name the container "factorio" (otherwise it has a random generated name).


To check the logs:

```
docker logs factorio
```

To stop the server:

```
docker stop factorio
```

Server Config (restart server after modifying)
* `server-settings.json` file in the folder `/factorio/config`.
* `map-gen-settings.json` file in folder `/factorio/config`.

## Saves

A new map named `_autosave1.zip` is generated the first time the server is started. The `map-gen-settings.json` file in `/factorio/config` is used for the map settings. On subsequent runs the newest save is used.

To load an old save stop the server and run the command `touch oldsave.zip`. This resets the date. Then restart the server. Another option is to delete all saves except one.

To generate a new map stop the server, delete all of the saves and restart the server.


## Mods

Copy mods into the mods folder and restart the server.



## Volumes

To keep things simple, the container uses a single volume mounted at `/factorio`. This volume stores configuration, mods, and saves.

    factorio
    |-- config
    |   |-- map-gen-settings.json
    |   |-- rconpw
    |   |-- server-settings.json
    |-- mods
    |   |-- fancymod.zip
    |-- saves
        |-- _autosave1.zip



## Ports

* `34197/udp` - Factorio clients (required).
* `27015/tcp` - RCON (optional).

# Factorio Vesions
For [(Dockerfile)](https://github.com/DDDGamer/factorio-server-docker/blob/master/Dockerfile)
(stable is default)

* `latest` - highest version: may be experimental.
* `stable` - highest version declared stable.
* `0.x` - highest version in a branch: may be experimental.
* `0.x.y` - a specific version.

# Credits

Ideas borrowed from:
* [dtandersen](https://github.com/dtandersen/docker_factorio_server)
