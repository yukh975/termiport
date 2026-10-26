# TermiPort

Terminal and SSH client for macOS with end-to-end encrypted sync.

Requires macOS 13.3 or later, Apple silicon or Intel.

🇷🇺 [Версия на русском](README.ru.md)

## Download

Get the latest version from [Releases](../../releases/latest):

- `TermiPort_VERSION_aarch64.dmg` — Apple silicon (M1 and later)
- `TermiPort_VERSION_x64.dmg` — Intel

What changed in each version: [CHANGELOG](CHANGELOG.md).

Open the .dmg and drag TermiPort to Applications. The app is not notarized
by Apple, so the first launch needs a one-time override: open TermiPort,
then System Settings ▸ Privacy & Security ▸ Open Anyway.

## Features

- SSH: hosts, groups, keys, jump hosts, known hosts, automatic reconnect
- Keys: file keys, Secure Enclave keys with Touch ID, FIDO2 security keys
- Agent forwarding through a built-in agent
- Port forwarding: local, remote, dynamic (SOCKS)
- SFTP
- Local terminal (the computer's own shell) and serial connections
- End-to-end encrypted sync

## Security and sync

- Everything is kept in a local vault encrypted with your master password;
  it can also be unlocked with Touch ID on that Mac.
- Sync is optional. Records leave the computer encrypted with a key that only
  your devices hold; the server never sees hostnames, usernames, keys or
  device names.
- A new device needs only the account password and the second factor, if
  it is on (an authenticator app or a FIDO2 key), and syncs at once.
- A recovery code is shown once when the account is created. Keep it for
  emergencies.

## Licenses

- Sync is free for up to 3 active devices per account. Revoked devices do
  not count.
- A license raises the device limit. It belongs to the account's email, not
  to a server, and works on any TermiPort server.
- Install it in **Settings ▸ License ▸ Install License…**.
- A license is valid until its end date or perpetual. An expired license
  keeps working for 14 days. After that the free limit applies again: the
  account's oldest devices keep full sync, the others become read-only.
  Nothing is deleted.

## Updates

TermiPort checks for a newer version at launch and on **TermiPort ▸ Check
for Updates…**, shows what changed and installs only updates signed by the
developer.

---

© 2026 Yuriy Khachaturian. All rights reserved.
