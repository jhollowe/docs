# Definitions

Within this (and the official Proxmox) documentation, there are some terms that may be confusing or unfamiliar to you. This page contains definitions and explanations of terms used. You can use the table of contents to the right to find a specific term or use the site search above to find documentation for a term.

## General

### [Authentication Realms](https://pve.proxmox.com/wiki/User_Management#pveum_authentication_realms)

Within Proxmox services is the idea of authentication realms. These realms are separate authentication systems which get their credentials from different sources. However, each supported realm can allow access to users within that realm for their configured resources.

PAM
:   The PAM realm is used by the default root account. The PAM realm uses the Linux users on the system to authenticate. This authentication realm requires the Linux user to exist in addition to creating the user within the Proxmox service. Since a user in this realm is also a Linux user, this realm allows use of SSH and shells. The passwords for this realm are managed by Linux and not the Proxmox service. Passwords for this realm can be changed by running `passwd` as the user or `passwd <username>` as a superuser (root).
