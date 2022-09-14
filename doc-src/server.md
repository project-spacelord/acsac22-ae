# Server Setup

Spacelord hub device communicates with an image server and the storage server.
The storage server can be any HTTP server
(e.g., [static-web-server](https://github.com/joseluisq/static-web-server),
[Python SimpleHTTPServer](https://www.digitalocean.com/community/tutorials/python-simplehttpserver-http-server))
that can serve static files.
The serving location should be
where `.lz4` compressed user images are.

Spacelord's storage encryption currently relies on iSCSI and WireGuard.
We provide a qcow virtual disk image for the storage server.
Download `storage-server/run-storage-server.sh` and `storage-server.qcow2.lz4`
in the same directory and execute `run-storage-server.sh` to run the storage server.
