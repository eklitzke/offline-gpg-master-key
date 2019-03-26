# Using Offline GnuPG Master Keys

This script is used to access an offline [GnuPG](https://www.gnupg.org/) master
key stored on an offline device (e.g. an [air
gapped](https://en.wikipedia.org/wiki/Air_gap_(networking)) USB key). The script
will prompt you to decrypt the master key and will then store the decrypted key
in a secure temporary directory. It will then invoke GnuPG with that temporary
directory as the GnuPG "homedir", and will ensure that the directory is removed
and the USB device is unmounted immediately afterwards.

Why would you need a script like this? The main reason would be do things like
using your offline master key to create new [GPG
subkeys](https://wiki.debian.org/Subkeys). If you're not already familiar with
them, GPG supports three kinds of subkeys: encryption, signing, and
authentication subkeys. Even if you're not aware, GnuPG creates at least one
subkey by default (the encryption subkey). Subkeys are an excellent way to use
GnuPG for day-to-day tasks without the risk of compromising one's master key.
They also allow users to revoke compromised keys and set sane expiration
policies on subkeys, as in the event of a lost or expired key a user can easily
generate new trusted subkeys from their secure master key.

The `offline-gpg-master-key` script here is written in Bash and uses various
Linux-specific commands to examine and mount block devices. I've tested this
code using GnuPG 2.2.x, and it probably works with other versions as well. If
you have any portability improvements to make, please send me a pull request.

This code is adapted from a script listed in Damien Goutte-Gattat's article
[Using an offline GnuPG master
key](https://incenp.org/notes/2015/using-an-offline-gnupg-master-key.html). If
you're not familiar with offline keys or subkeys in general, or want to
understand how this script works, I highly recommend reading Damien's article.
In fact, you should probably read it even if you are familiar with them. The
main modifications in the script I've written here are various options to add
additional flags, error checking, and help messages.

This code is free software, released under the terms of the GPLv3+.
