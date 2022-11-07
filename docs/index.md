<!-- spell-checker:ignore Proxmoxia -->
# Welcome to Proxmoxer

Proxmoxer is a wrapper around the APIs for Proxmox products.

Proxmoxer handles all the authentication, path building, and data communication so you can focus on your goals. It requires no updates for new Proxmox versions as there are hardcoded paths; your code defines how you want to interact with Proxmox and proxmoxer just facilitates.

## Supported Services

Below are the Proxmox services supported by this library.[^1]

* PVE ([API Spec](https://pve.proxmox.com/pve-docs/api-viewer/index.html))
* PMG ([API Spec](https://pmg.proxmox.com/pmg-docs/api-viewer/index.html))
* PBS ([API Spec](https://pbs.proxmox.com/docs/api-viewer/index.html))

## Supported Backends (Connection Methods) {#supported-backends}

The following backends are supported:[^1]

* HTTPS
* SSH (openssh)
* SSH (ssh_paramiko)
* local

View the [Setup](setup/) page for details on how to setup your environment for each backend.

[^1]: The names of the services and backends can be in any case as the library will standardize the case to what it requires. e.g. "hTtpS" is just as valid as "https" or "HTTPS".

--8<-- "abbreviations.md"
