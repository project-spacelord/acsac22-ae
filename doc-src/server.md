# Server Setup

Spacelord hub device communicates with an image server and a storage server.
The image server can be any HTTP server
(e.g., [static-web-server](https://github.com/joseluisq/static-web-server),
[Python SimpleHTTPServer](https://www.digitalocean.com/community/tutorials/python-simplehttpserver-http-server))
that can serve static files.
The serving location should be
where `.lz4` compressed user images are.

Spacelord's remote encrypted storage utilizes iSCSI and WireGuard.
We provide a qcow virtual disk image for the storage server.
Download `storage-server/run-storage-server.sh` and `storage-server.qcow2.lz4`
in the same directory and execute `run-storage-server.sh` to run the storage server.

Currently, `run-storage-server.sh` assumes that it can forward host port 51820
to the storage server for WireGuard communication. If host port 51820 is
reserved for other purposes, both `run-storage-server.sh (hostfwd)` and
`config.toml (WG_LISTEN_PORT)` should be revised accordingly.
