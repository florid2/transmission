# Transmission

Transmission docker container

# What is Transmission?

Transmission is a BitTorrent client which features a simple interface on top of
a cross-platform back-end.

## Hosting a Transmission instance

    sudo docker run -it --name transmission -p 9091:9091 -d florid2/transmission

OR set local storage (see *Complex configuration* below):

    sudo docker run -it --name transmission -p 9091:9091 \
                -v /path/to/directory:/var/lib/transmission-daemon \
                -d florid2/transmission

**NOTE**: The configuration is in `/var/lib/transmission-daemon/info`, downloads
are in `/var/lib/transmission-daemon/downloads`, and partial downloads are in
`/var/lib/transmission-daemon/incomplete`.

## Configuration

    sudo docker run -it --rm dperson/transmission -h

    Usage: transmission.sh [-opt] [command]
    Options (fields in '[]' are optional, '<>' are required):
        -h          This help
        -n          No auth config; don't configure authentication at runtime

    The 'command' (if provided and valid) will be run instead of transmission

ENVIRONMENT VARIABLES (only available with `docker run`)

 * `TRUSER` - Set the username for transmission auth (default 'admin')
 * `TRPASSWD` - Set the password for transmission auth (default 'admin')
 * `USERID` - Set the UID for the app user
 * `GROUPID` - Set the GID for the app user

Other environment variables beginning with `TR_` will edit the configuration
file accordingly:

 * `TR_MAX_PEERS_GLOBAL=400` will translate to `"max-peers-global": 400,`

## Examples

Any of the commands can be run at creation with `docker run` or later with
`docker exec -it transmission.sh` (as of version 1.3 of docker).
