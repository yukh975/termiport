# Changelog

All notable changes to TermiPort, newest first. Format based on
[Keep a Changelog](https://keepachangelog.com/); versions are
`YY.M.D.N`.

🇷🇺 [Версия на русском](CHANGELOG.ru.md)

## 26.10.26.35

### Added

- SFTP tabs have a Disconnect button in the host pane, next to its name, and a Disconnect item in the tab's context menu. It closes the connection and keeps the tab, which shows `Session closed` with Close and Reconnect; the tab does not reconnect by itself, even when Reconnect is on for the host. When transfers are running it asks first and cancels them. It is disabled until the tab is connected.
- Each SFTP pane has Back (⌘[), Forward (⌘]) and Up (⌘↑) buttons before the filter field, with the keys in their tooltips, and its own history of the folders it has shown. Back and Forward are disabled when there is nowhere to go, and Up is disabled at `/`. Going to a folder by a row, a breadcrumb, a typed path or Up adds the folder you left to the history and clears Forward; Refresh and a folder that cannot be opened do not change it. ⌘[ and ⌘] work in the file list like ⌘↑ does.

## 26.10.26.34

### Added

- SFTP tabs. The new SFTP section of the sidebar (⇧⌘F by default, also Shell ▸ SFTP) lists the hosts; Enter opens an SFTP tab to a host, and the search field takes `user@host:port`. Open SFTP is in the host's context menu and in the context menu of an SSH tab, which opens the SFTP tab right after it; an SFTP tab has Open SSH in its menu. The tab has two panes, this computer and the host, each with breadcrumbs, a filter field that also takes a typed `/path` or `~`, hidden files on demand, sorting by name, size or modified time, and a list that takes the keyboard: arrows, ⇧ to extend, ⌘A, Enter, ⌥↩ to copy the selection to the other pane, ⌘↑ for the parent folder, ⌘I for Info and ⌘⌫ to delete on the host.
- New Folder on both sides; Rename, Delete and Info on the host; Info and Show in Finder on this computer.
- Drag and drop. Files and folders dragged from Finder onto the host pane upload into the folder under the pointer (a folder row, or the folder the pane shows), which is outlined while the pointer is over it; a drop anywhere else on an SFTP tab does nothing. Between the panes, pressing a row and moving 4 px drags the selection with a label that follows the pointer (`report.pdf`, or `3 items`); releasing over the other pane's list or a folder row copies there, and releasing anywhere else or pressing Esc cancels.
- Download to… in the context menu of a host row copies the selection into a folder chosen in the system dialog, and the result line of a finished download has Show in Finder.
- On macOS every file a download writes to the computer gets the `com.apple.quarantine` attribute, as a browser download does, so macOS checks it before it is opened for the first time. Uploads and folders are not marked.
- Upload and Download of files and folders with a queue per tab, progress with the speed, Cancel and Cancel All, and a result line. A name that already exists asks what to do: Stop, Skip, Keep Both, Replace for a file or Merge for a folder, each with Apply to all. A file that fails asks Stop or Skip. Files are written under a temporary name and renamed when complete. A tab with a transfer asks before it closes, and so does Quit.

### Changed

- The sidebar has Terminal, Serial and SFTP above the divider, then Hosts, Keys and Known Hosts; Serial moved up from below the divider.

## 26.10.26.33

### Added

- Auto-lock: the vault locks the same way as Lock Vault after a period without input (15 minutes by default; 1 minute to 4 hours or never, in Settings → Security) and when the computer locks or sleeps (can be turned off there). Terminal output does not count as activity; open connections stay up, as with Lock Vault.

## 26.10.26.32

### Added

- More… in the Serial quick connect holds the rest of the port settings: data bits, parity, stop bits, flow control, what Enter sends, local echo, logging and reconnect. The values are remembered on this computer, a reconnect of the tab keeps them, and Save as Profile… fills the editor with all of them.

## 26.10.25.31

### Added

- Serial connections. The new Serial section of the sidebar (⇧⌘S by default, also Shell ▸ Serial) has quick connect, where you choose a port from the live list (Other… takes a typed path) and a baud rate and press Connect, and saved profiles: name, port, baud rate (Custom… takes 50–4000000), data bits, parity, stop bits, flow control (none, XON/XOFF, RTS/CTS), what Enter sends, local echo, logging and reconnect. A profile has its own editor, Connect, Edit…, Duplicate and Delete… in its context menu, and syncs, backs up and restores with the rest of the vault. Save as Profile… in a quick connect tab's context menu opens the editor filled in with what the tab uses.
- A serial profile remembers the USB identity of its port. When the saved path is gone, Connect opens the one listed port with the same identity and the tab says where the device is now; with no such port, or with several, the tab shows an error with Edit Profile…. A port is opened exclusively, so one that is in use is reported, not shared.
- The context menu of a serial tab: Reconnect, Send Break, DTR and RTS, Start Logging / Stop Logging, Show Log in Finder, Edit Profile… or Save as Profile…, Close. When the device is unplugged, the tab says "the device was disconnected"; with reconnect on it shows "Disconnected: … Waiting for the device…", looks for the device every second and opens it again with the logging, DTR and RTS it had; Cancel stops the wait.
- Session logs of a serial tab: the bytes the device sent, one file per opened session, switched per profile and from the tab. Settings gets a Serial section with the Log folder (Choose…, Use Default, Show in Finder); the default is `~/Library/Logs/TermiPort/Serial`. Logs are not encrypted and hold everything the device sent.
- Keyboard shortcuts you can change. Settings gets a Keyboard section that lists every command of the menu and the tab bar with its shortcut: click a field and press the new keys, ⌫ removes the shortcut, Esc cancels, Reset restores one row and Reset All, after a confirmation, all of them. A change works at once in every window and in the menu and survives a restart; the shortcuts are kept on this computer and are not synced. Quit (⌘Q) and Select All (⌘A) cannot be changed, every other shortcut needs ⌘ (⌃Tab excepted), and a refused shortcut names its reason: a standard menu item, a macOS key, a list key (⌘I, ⌘D, ⌘⌫, ⌘↑) or the command that already has it. Keys are taken by the physical key, so a shortcut recorded on a Russian layout works on any layout. Show Hosts Tab, Show Tab 2 … 8, Show Last Tab and Cycle Tabs can be changed too.
- Export Settings… and Import Settings… in Settings ▸ General, for moving the settings to a new computer. `TermiPort Settings.json` holds the terminal settings, the agent settings, the serial log folder and the shortcuts, and nothing from the vault, the sync account, the license or the security settings. Import asks first and lists what it will change, including the agent settings and a shortcut that loses its key to the file; it needs the vault unlocked. A setting missing from the file keeps this computer's value, what this version does not know is skipped and listed, and one invalid value refuses the whole file and changes nothing.

### Changed

- The sidebar has Terminal at the top, separated by a divider from Hosts, Serial, Keys and Known Hosts. Terminal opens a local terminal (⌘T by default); the shortcuts of Terminal, Hosts, Serial and Keys show in their tooltips. The "+" button is gone from the tab bar, and Shell ▸ New Tab is now New Terminal.
- Hosts, Serial and Keys lists take ⌘I (edit; Rename… in Keys) and ⌘⌫ (delete) by the physical key, Hosts and Serial also ⌘D (duplicate), and Hosts also ⌘↑ (parent group), so they work on a non-Latin layout. The shortcuts of the menu and of the tooltips come from one table.

## 26.10.25.30

### Added

- Port forwarding rules on hosts: local, remote and SOCKS (4, 4a and 5). The host editor gets a Port Forwarding section; Add Forward… opens a sheet with the type, a label, the listen address and port, the destination and "Start with the connection". Listening on an address other than loopback shows a warning. A host can have up to 64 rules; they sync, back up, restore and duplicate with it.
- Rules with "Start with the connection" start when a terminal tab to the host connects. The tab's context menu has Port Forwarding…, a dialog to start and stop each rule that shows its state, the addresses it listens on and its open connections. A rule that fails to start with the connection also shows a notice in the tab. A tab running forwards shows ⇄ after its title; a host with rules shows ⇄ in the list, and the search matches rule labels.
- Tunnel tabs: Open Tunnel in the host's context menu connects without a terminal and starts the host's "Start with the connection" rules, or all of them when none has it; Start Forward starts one rule. A rule runs in one tab at a time; starting it in another tab says it is already running there.
- After an automatic reconnect the rules that were running start again.
- A forwarded connection whose program on this computer stops reading is closed once 16 MiB of its data is waiting and nothing has been read for 10 seconds, and the rule's state says why; while it waits, the tab's terminal and other rules pause.
- Import from `~/.ssh` turns `LocalForward`, `RemoteForward` and `DynamicForward` into rules, applying `GatewayPorts` and `ClearAllForwardings` as OpenSSH does; forms TermiPort does not run (Unix sockets, `RemoteForward` without a destination, port 0, `${VAR}`) stay in the host notes. The import summary counts the rules.

## 26.10.23.29

### Added

- License revocation list. The vendor adds revoked licenses to a signed list (`termiport-license revoke`), the developer's server serves it, and the app, after each update check, passes it to its sync server, which revokes every license on it, also from a list older than the one it keeps, and revokes the licenses of the kept list again at start. A server never connects anywhere for the list itself; the admin can also install it with `license revocations install FILE`, and `license revoked` shows the installed list.

### Changed

- Update notes are signed separately from the archive. The app shows the notes of an update only when their signature verifies; an update whose notes are not signed is offered without them.

### Fixed

- Cancel or Esc on the connect card of a tab that was connected before, and locking the vault while such a tab reconnects, stop the attempt and keep the tab with its output, under the Disconnected bar; before, the tab closed. A tab that never connected still closes.
- An address typed in the Hosts search can be connected even when it is part of a saved host's address (`10.0.0.1` with `10.0.0.10` saved): text with `.`, `:` or `@` gets a quick-connect row below the matching hosts unless it is exactly a saved host's name or address.
- A session that ended with an exit status is shown as ended, not as a dropped connection, also when the server closes the connection without closing the channel, and a session closed without an error is shown as closed; neither reconnects.
- When the server breaks the connection during sign-in (for example, after too many authentication failures), the tab reports a sign-in error and does not reconnect.
- Saving a backup writes a new file and puts it in place of the old one only once it is complete; before, a failed write (full disk, removed drive) could leave neither copy.
- A damaged Termius database no longer crashes the app during import; the import reports an error.
- Erase All also removes Secure Enclave keys that have no key record left; before, the app kept offering to restore them.
- Closing the Termius import, SSH import or backup dialog drops what it read (Termius passwords and keys, backup contents) at once, and Termius passwords and private keys are zeroed when freed; before, they stayed in memory until the vault was locked or the next scan.
- Adding a device with the sync password has its own limit of five tries a day, and a correct password does not count; before, it used up the tries of the recovery code even when the password was right. When the tries run out, the app falls back to approval from another device, as for a wrong password.
- The account's address gets a letter when a device joins with the sync password, and one for every device removed because a new device took its place on the same computer after approval or recovery; before, both happened without a letter.
- With PostgreSQL, the server gives up on connecting to the database after 5 seconds unless `connect_timeout` is set, and a request that waits more than 10 seconds for a free connection fails instead of waiting forever.
- With PostgreSQL, a connection whose request was dropped while waiting for its turn to write is closed instead of going back to the pool, where the next request would have waited behind it.
- PostgreSQL errors in the server log leave out the error detail, which can hold values from the rows; the code, message, table and constraint stay.
- `import-sqlite` no longer writes to the SQLite file: it reads it as one snapshot and refuses a file from another version instead of bringing it up to date.
- The server writes update descriptions and the revocation list through a temporary file of its own and flushes the directory after the rename; before, two writers at once shared one temporary file, and a power loss right after a write could lose it.
- Making a backup no longer leaves pieces of the unencrypted contents in freed memory while the buffer grows.

## 26.10.23.28

### Changed

- The Server address field of sync setup comes filled in with the TermiPort sync server; another address can be typed over it.

## 26.10.23.27

### Added

- Host and group setting Reconnect: when the session in a tab drops, the tab connects again after the set pause (1–3600 s, 10 by default) and keeps trying while the error is one a retry may fix (the network, a timeout, a jump host). The bar shows the countdown with Reconnect Now and Cancel. Off unless turned on.

### Changed

- Enter in the Hosts search field connects only when the list has a single row; with several matches it does nothing. Before, it opened the first of them.

### Fixed

- The bar at the bottom of an ended session no longer covers the last lines of the terminal.
- The host editor shows Forward agent and Forwarded keys inherited from the group; before, they read as the default.
- Reconnecting a tab goes on below the earlier output; before, the new session was written over it from the top of the screen.
- With PostgreSQL the server no longer logs a notice that `termiport_schema` already exists at every start and every command.

## 26.10.23.26

### Added

- Settings ▸ General ▸ "Close the tab when its session ends without an error". Off by default.

### Changed

- When the session in a tab ends (the shell exits, the connection drops), the tab stays open with its scrollback: the terminal shows "[session closed]", and the bar at the bottom offers Close and Reconnect. A program cut off while it held the whole screen (an editor, `top`) no longer hides the scrollback. Before, the tab closed when the shell exited without an error; the new setting brings that back.
- Pressing ⌘W again in the Close “…”? dialog closes the tab, as ⌘Q does in Quit TermiPort?. The second press counts only half a second after the dialog opens.
- Clicking Synced at the bottom of the sidebar syncs at once and shows Syncing until it ends; before, it opened Settings ▸ Sync. Sync Needs Attention still opens Settings. While sync is off the sidebar shows Not syncing, which opens Settings ▸ Sync to set it up.
- The first tab no longer sits right against the window buttons.

## 26.10.23.25

### Added

- Perpetual licenses: `termiport-license issue --perpetual` instead of
  `--until` issues a license that never expires. The app shows it as
  valid with no end date, `license show` and `license list` on the server
  as perpetual.
- Revoking a license on the server: `license revoke EMAIL|ID` removes the
  license from its account and refuses to install it again;
  `license revoked` lists the revoked licenses. `license remove` still
  only takes a license off an account.
- The About window shows the account's license: who it is issued to and
  until when, or the free plan.
- The server can keep its data in PostgreSQL: `[database] postgres` in
  the config (or `TERMIPORT_SERVER_DATABASE_POSTGRES`) takes a connection
  string, and the server creates and migrates its tables there. Empty
  keeps SQLite in `server.db`. `server.key` stays in the data directory
  with either. `[database] password_file` reads the password from a file,
  like `smtp.password_file`.
- `termiport-server import-sqlite [FILE]` copies an SQLite database into
  an empty PostgreSQL one in a single transaction; devices keep their
  tokens.

### Changed

- `termiport-server backup` refuses with PostgreSQL: back up with
  `pg_dump` and copy `server.key`.
- The systemd unit starts after `postgresql.service`.

## 26.10.23.24

### Changed

- Without a license an account syncs up to 3 active devices instead of 2.
- The public README on GitHub has a Licenses section: the free limit,
  what a license gives, how to install it and what happens when it expires.
- The READMEs now say that a new device signs in with the password and the
  second factor; approval from a connected device is only a fallback.
- The public GitHub repository keeps only the latest release:
  `scripts/publish-github.sh` deletes older releases and their tags.
- The public GitHub repository has the CHANGELOG in English and Russian,
  and its README links to it.

### Fixed

- Locking the vault in the middle of a sync could briefly leave the old
  sync status on screen instead of “locked”.

## 26.10.23.23

### Added

- `termiport-server license list` shows every account with a license: license id, state and active devices against the limit.
- Every release has the license tool for macOS, `termiport-license-VERSION-macos-aarch64` and `-macos-x64`, next to the .dmg files, so licenses can be issued without Rust. `scripts/publish-mac.sh` uploads the macOS files and attaches them to the release.
- Intel Macs: every release has `TermiPort_VERSION_x64.dmg` next to the Apple silicon `TermiPort_VERSION_aarch64.dmg`, and each app updates to the build for its own processor.
- Releases are also published to a public GitHub repository: the .dmg files with the changelog in English, and a README for users. `scripts/publish-github.sh` publishes them after `publish-mac.sh`.

### Changed

- The sign-up form asks for an invite code only when the server signs up by invitation.
- Updates come from the developer's server whether sync is on or not; the update dialog no longer sends you to set up sync. A self-hosted sync server does not serve updates. Update checks and downloads need no account and are limited to 60 an hour per IP address.

## 26.10.23.22

### Changed

- The license has its own Settings tab, Settings → License, instead of a section in Settings → Sync. Without sync it explains that the license belongs to the sync account and opens the Sync tab.

## 26.10.23.21

### Changed

- Licenses belong to users, not servers. Any server, the main one or a self-hosted one, takes any number of accounts for free, each with 2 active devices; a license issued for an account's email raises that account's device limit on whichever server it uses, and changes nothing for other accounts.
- Settings → Sync → License shows the account's license, its expiry and the active devices against the limit; **Install License…** installs a license file.
- Server: `license install FILE` installs a license on the account with the license's email, `license show EMAIL` and `license remove EMAIL` show and remove it. `account plan` is gone; the `mode` and `[hosted]` settings are ignored with a warning in the log.
- The server trusts the TermiPort vendor key, so it accepts licenses signed with it; before, every license was refused.

### Fixed

- The Hosts search no longer adds a "Connect to …" row under the hosts it found; quick connect is offered only when no host matches.
- The "agent forwarding is on" message is now a line in the terminal before the shell's output; it was a notice over the terminal that hid the first lines of the prompt.

## 26.10.23.20

### Added

- **Back Up…** (Shell menu) saves hosts, groups, keys with their passphrases, saved passwords and known hosts to a file encrypted with a backup password of at least 8 characters. The password does not depend on this computer, so the backup restores on any device. Secure Enclave keys stay out: they cannot leave the Mac.
- **Restore from Backup…** (Shell menu) opens a backup with its password, shows what it holds and adds only what is missing: nothing already here is deleted or overwritten, and links between hosts, groups and keys are kept.
- Settings → Sync shows the server license: its state, expiry, grace period, limits, current usage and how to renew it.
- In-app updates through the sync server: with sync on, TermiPort looks for a newer version at launch and on **TermiPort → Check for Updates…**, shows what is new and installs it with one click, then restarts. Only updates signed by the vendor's key install. Without sync, the dialog points to Settings → Sync.
- Server: `termiport-server update install MANIFEST ARCHIVE` serves an app update to devices, `update show` lists what is served.

## 26.10.22.19

### Added

- Select several hosts and groups with ⌘-click, Shift-click, Shift-arrows or ⌘A and delete them together; deleting a group takes its subgroups and hosts with it.
- **TermiPort → Erase All Data…** deletes every host, group, key and known host on this computer and on every device that syncs with it. Sync settings stay.

### Changed

- Import and Import from Termius… moved from the Hosts sidebar to the Shell menu: they bring in keys and known hosts too, and the buttons no longer vanish once hosts exist.
- A group row counts the hosts in all its subgroups and shows how many subgroups it has, instead of only the hosts placed directly in it.

## 26.10.22.18

### Added

- **Import from Termius** (macOS): Hosts → Import from Termius… reads the local Termius vault and brings over groups with their defaults, hosts with user, port, password and key, keys with their passphrases (FIDO keys become security keys), and known hosts. Tags and snippets go to the host's Notes. Running it again adds only what is missing. macOS asks once for access to the Termius key in the Keychain.

### Fixed

- If signing in to sync fails after the second factor is accepted — a lost connection, an outdated server — Continue now retries without a new code instead of reporting that the sign-in challenge expired.
- If signing in fails right after a sync password reset, the sign-in form comes back with the new password instead of leaving the spent reset code on screen.
- A sync server too old for the app now says it needs an update instead of reporting "not found".

## 26.10.22.17

### Changed

- Closing a tab with the mouse — the ×, a middle click or the context menu — asks for confirmation, as ⌘W does, while its session is alive.
- `invite list` shows when a used code was used instead of its expiry; an expired one shows `expired` with the date.

### Fixed

- After a sync password reset, signing in on another computer with the new password and the second factor no longer waits for approval from another device. Needs the updated sync server.
- Reinstalling TermiPort or signing in to sync again on the same computer replaces that computer's old device instead of leaving it behind and taking another seat. Needs the updated sync server; devices left over from earlier builds are removed by hand in the device list.
- The Settings window keeps one size on every tab instead of resizing to each page.
- In Settings → Security, each row label now sits level with the first line of its data instead of floating above it.
- Settings → Security row labels use the muted colour, so a label is no longer the same colour as the data beside it.
- The Settings section tabs no longer sit flush against each other: there is space between them.

## 26.10.22.16

### Added

- Server administration: `invite list` shows every issued code with its address, dates and status, and `invite revoke EMAIL` drops an address's still-active codes. The old `invite` command is now `invite issue`.

### Changed

- Settings open in tabs — General, Security, Agent and Sync — so no page is crowded or scrolls.
- The accent color follows the terminal theme instead of a fixed blue, so the window keeps one palette.
- **Version format is `YY.M.D.N`** (was `YY.M.D build N`). Git tags: `vYY.M.D.N`.

### Fixed

- A "too many attempts" message now says how long to wait before trying again.
- Mail from the sync server arrives in the app's language, not the computer's.

## 26.10.22 build 15

### Added

- Forgot Password? on the sync sign-in form: the server mails a reset code, or its administrator issues one. After the new password the app asks for the second factor again if the account has one; a recovery code used for the reset also adds this device.

## 26.10.22 build 14

### Changed

- The sync server packages are built for every release and attached to it.

### Fixed

- The sync password hint no longer says the password protects the account keys: it is for signing in only, and your data opens with your devices or the recovery code.

## 26.10.22 build 13

### Added

- Packages for the sync server: a Docker image, deb for Debian 12 and 13, rpm for ALT p11 and Sisyphus, with a hardened systemd service.
- Server administration: `device list EMAIL` and `device revoke EMAIL DEVICE_ID`. Revoke signs the device out, asks the other devices to rotate keys and mails the user.
- Server settings `[connections] max` (default 1000) and `[connections] waits_per_account` (default 16).

### Changed

- The sync server refuses to run as root on a data directory owned by another user, and requires `public_url`.

### Fixed

- Device approval: the sync server can no longer slip in its own key or a different approving device. If the approving device changes, TermiPort asks you to compare the codes again.
- After a device is revoked, the server can no longer cancel the key rotation.
- The server checks rosters signed with the recovery code against the account's recovery key.
- Recovery works when the account is at its device limit; the recovered device is read-only until a lost device is revoked.
- An admin-revoked device no longer breaks key rotation; it leaves the device list at the next rotation.
- Server: parallel guessing no longer gets past the limits on sign-in, second factor, password confirmation and password reset; failed second factors during a reset count too.
- Server: someone guessing your password no longer blocks password confirmation on your own devices.
- Server: password hashing, connections, request headers and the per-address limits are bounded, so a flood of requests cannot exhaust its memory or open files.
- Server: email changes are limited to 5 a day per account.
- Sync warnings (older data on the server, recovered device, rotation due) stay until dismissed, also across lock and restart.
- Records this device cannot open no longer stop re-encryption after a key rotation.
- An approval opened in another window shows the codes too, instead of waiting with Approve disabled.
- If the vault locks during an approval, the approval closes with a note to start again on the new device instead of returning on every unlock.
- Locking the vault while signing out or confirming the password no longer leaves a hidden prompt that blocks tab shortcuts and menu commands.
- Turning on the authenticator code asks for the sync password again if the confirmation has expired, instead of failing.
- The question about replacing the sync recovery code appears once per unlock, not once per window.
- If the saved sync settings cannot be read, sync shows as out of date instead of locked; Sign Out and the vault password change work again.

## 26.10.22 build 12

### Added

- Sync between devices through your own server (Settings ▸ Sync): sign in or create an account with email and password, with an optional authenticator code or security key. Data is end-to-end encrypted; the server sees only ciphertext.
- A new device joins only when an already signed-in device approves it after both show the same code, or with the sync recovery code.
- Sync devices list with Rename and Revoke; Security with two-factor, password, email and recovery code changes; Delete Account.
- Sync status indicator in the sidebar.
- The sync server `termiport-server`: free for one account and two devices, more with a license.

### Fixed

- After unlocking with the recovery code, the app asks for a new code again on every unlock until it is replaced, even after a restart or a lock.
- If the vault locks while a new recovery code is on screen, the next unlock asks to replace it, since that code may never have been stored.
- Add Backup Key with a mistyped recovery code fails at once, before the new key is inserted and touched.
- Dialogs opened from Settings no longer reappear by themselves after a lock and unlock.
- In password mode, Use a Security Key Instead of the Password no longer disappears from Settings after a lock and unlock.
- An update from the old TermPort build no longer starts with an empty vault when the old build was running at the first launch.

## 26.10.21 build 11

### Changed

- Pressing ⌘Q again in the Quit TermiPort? dialog quits. A quick double press does not: the second press counts only half a second after the dialog opens.

## 26.10.21 build 10

### Fixed

- Remove on the only security key in Settings now opens Switch Back to Master Password instead of being greyed out.
- Dialog buttons no longer touch the bottom edge when the dialog scrolls, as in Settings.

## 26.10.21 build 9

### Fixed

- The Touch ID button on the lock screen no longer sits flush against the security key button or the password field.

## 26.10.21 build 8

### Changed

- The lock screen no longer starts Touch ID by itself: it waits for the master password or a press of the Touch ID button.

## 26.10.21 build 7

### Added

- The master password can be backed by a code from an authenticator app (TOTP): Settings → Security → Ask for an authenticator code. Setup shows a QR code and the key as text; turning it on needs the master password and a code from the app. After the password, TermiPort asks for the 6-digit code before it shows the vault or lets the agent serve keys. A one-time recovery code is shown at setup: it replaces the code once if the app is lost and turns the code off. Wrong codes make you wait longer and longer, up to 5 minutes. Touch ID unlock does not ask for the code, and switching to a security key removes it. The code does not encrypt the vault: a copy of the vault file still opens with the password alone.
- The About window shows the copyright (© 2026 Yuriy Khachaturian, all rights reserved) and a link to yukh.net. The app bundle carries the same copyright, and the repository has a LICENSE file.

### Changed

- Touch ID unlock now works together with a security key. With a key enrolled the vault opens only with that key, a backup key or the recovery code, and the password is off; Touch ID unlock can stay on. The lock screen offers it next to the key, and turning it on in Settings asks for a touch of one of the enrolled keys. Touch ID stays on when you switch between the password and a security key. If the key it was set up with is removed with the recovery code, Touch ID unlock turns off and asks to be turned on again.
- Turning on a security key now warns that afterwards the vault opens only with this key or a backup FIDO2 key added later, and that password unlock (together with the authenticator code) is turned off, while Touch ID unlock stays on.

## 26.10.21 build 6

### Added

- Quit (⌘Q) asks for confirmation first, so a slip of the finger no longer ends every session. Closing a tab with a live session (⌘W) asks too; tabs whose session has already ended close at once. Cancel is the default button.
- Creating the master password offers Touch ID unlock right away (the checkbox is on by default when the Mac has Touch ID with a fingerprint enrolled), so it no longer has to be turned on later in Settings.
- Settings → Security has a Change Master Password… button (the same dialog as in the TermPort menu).
- A hardware security key (FIDO2, for example YubiKey) can replace the master password: Settings → Security → Use a Security Key Instead of the Password. The vault then opens with the key and its PIN; up to 8 keys can be enrolled as backups, and an optional one-time recovery code opens the vault when no key is at hand (TermPort then asks to replace it). Touch ID is not used in this mode. Switching back to the master password sets a new password.

### Changed

- The app is now called TermiPort (bundle id `app.termiport.desktop`). On first start it moves the data of the old TermPort (vault, keys, agent socket, settings) to the new place and leaves a link at the old path, so `IdentityAgent` lines in `~/.ssh/config` keep working. If the old TermPort is still running, its data is used in place and moved on the next start. Environment variables are now `TERMIPORT_*`.
- While TermPort is locked, local terminal tabs keep working: you can type in them and open, switch and close tabs. Only hosts, keys and connections stay locked; the lock screen now appears in the Hosts tab and over SSH tabs instead of covering the whole window. Settings ▸ Agent can be viewed but not changed until you unlock.

### Fixed

- Interface text (tabs, menus, panes and dialogs) no longer takes the terminal theme's text colour as is: with bright themes such as Homebrew it was glaring green. It now uses a soft neutral colour with a slight tint of the theme, and panel backgrounds are neutral grey.
- The Font size in Settings now scales the interface text too, not only the terminal.
- Tabs stand apart from each other and from the tab bar: each tab has its own lighter background with a gap between tabs, and the active tab is the lightest.
- A security key that is not touched in time is now reported as a timeout, not as a refusal (YubiKey answers “operation denied” when the wait runs out).
- Cancelling a security key request now stops the key at once: it stops blinking and is free again, instead of waiting for a touch for about 30 more seconds.
- Field and checkbox labels in Settings and other dialogs are now as bright as the values next to them; before they were dimmed and hard to read.

## 26.10.21 build 5

### Added

- Built-in SSH agent: programs such as `ssh` and `git` can use the keys in the vault through TermPort's agent socket. Settings ▸ Agent shows the socket path and the two lines to copy: `export SSH_AUTH_SOCK=…` for the shell and `IdentityAgent …` for `~/.ssh/config`.
- Local tabs get `SSH_AUTH_SOCK` pointing at the agent, so `ssh` in a local tab uses the vault keys (can be turned off in Settings ▸ Agent).
- When a program asks the agent for a key, TermPort can ask first: "Allow … to sign in to … with key …?" (Enter and Escape deny; always for forwarded requests, except with keys that ask for Touch ID or a touch themselves, and for local programs when "Ask before each use of a key by a local program" is on). It also asks for a key's passphrase when one is needed, and, while the vault is locked, offers to unlock it ("When the vault is locked": Ask to unlock or Refuse). If no TermPort window is open, the main window opens with the question.
- Settings ▸ Agent: turn the agent on or off, restart it, choose what happens while the vault is locked, and see the recent agent requests.
- Agent forwarding per host and group: "Forward agent" (off by default, inherited from groups) lets programs on the remote host, such as `ssh`, `git` or `sudo` through `pam_rssh`, use your keys while you are connected; "Forwarded keys" chooses which keys it offers (this host's keys, all keys or chosen keys). Requests from a forwarded agent are asked about in the tab, with the tab's name in the question; a tab with such a question is marked as waiting and adds "— waiting for input" to the window title, and closing the tab ends its forwarded requests. Host cards show a "forwards agent" badge.
- Import from ~/.ssh takes `ForwardAgent yes` and `no` into the host's "Forward agent" (a `no` is stored on the host when it would otherwise inherit forwarding from its group); a socket path or variable as the value turns forwarding on with a warning, and `IdentityAgent`, `SecurityKeyProvider` and `AddKeysToAgent` are skipped with a warning (`AddKeysToAgent` in the system file is still skipped without one).
- Secure Enclave keys: Keys ▸ + Key ▸ Create Secure Enclave Key… makes a key that never leaves this Mac's Secure Enclave, protected by Touch ID or the Mac's password, by Touch ID only, or (under Advanced) with no prompt. Sessions and the agent sign with it; Touch ID is asked for in the tab with Skip This Key and Cancel, or by the agent for programs, and a key with no prompt is confirmed like a software key. Locking the vault closes a Touch ID request the agent is showing.
- A vault copied to another Mac marks its Secure Enclave keys as not usable there ("Not usable on this computer", "On <Mac name>"); such keys can be hidden on this computer (Hide on This Computer, Show on This Computer), and hidden keys are left out of the host and group editors.
- Recovered keys: a Secure Enclave key found again after its entry was lost can be restored with Restore Key….
- The Keys pane shows each key's kind (Secure Enclave), its protection, whether it is offered in the agent (Offer in Agent in the key's menu) and whether it is usable on this computer.
- Shell ▸ Keys (⇧⌘K) opens the Keys pane, and pressing it again goes back to the hosts.
- Touch ID unlock: Settings ▸ Security ▸ "Unlock with Touch ID" (turned on with the master password, per computer) lets the lock screen open the vault with Touch ID. The lock screen asks for Touch ID by itself once per lock in the focused window and has an "Unlock with Touch ID" button; the master password always works too.
- While the vault is locked, the agent unlocks it with Touch ID when Touch ID unlock is on, and the unlock card's Unlock button starts Touch ID.
- When Touch ID unlock stops working (the master password was changed by an older TermPort, the Touch ID fingerprints changed, or the vault came from another Mac), the lock screen and Settings ▸ Security say why and how to turn it on again; a Touch ID unlock set up by a newer TermPort is left untouched and reported as such.
- Security keys (FIDO2, such as YubiKey): Keys ▸ + Key ▸ Create Security Key… makes an `ecdsa-sk` or `ed25519-sk` key on a plugged-in security key, with a choice of device when several are plugged in and, under Advanced, the application, storing the credential on the key, requiring the PIN on every use and not requiring a touch.
- Keys ▸ + Key ▸ Import from Security Key… lists the SSH credentials stored on a security key (after asking for its PIN) and adds the chosen ones to the vault.
- `id_ecdsa_sk` and `id_ed25519_sk` files are imported as security keys, by Import Key… and by Import from ~/.ssh, which also links them to the hosts that use them.
- Sessions and the agent sign with security keys: the tab or the window asks you to touch the key, for its PIN when needed (with the number of attempts left after a wrong PIN) and which key to use when several are plugged in and none holds the credential; a key that signs without a touch is confirmed before each forwarded use.
- When TermPort is not in front, a notification "Touch your security key: …" says that a security key is waiting for a touch.
- A security key that another program is using shows as "(busy)" in Create Security Key…, and creating a key on it or importing from it says that the key is busy.
- The PIN and key-choice questions of an agent request close on their own after the same wait as its confirmation, so an unanswered question does not hold up other security key requests.

### Fixed

- When the group chosen in Import from ~/.ssh, in the host editor or as the parent in the group editor is deleted (for example in another window), the choice moves to All Hosts (for a group being edited, back to its current parent) with a note saying so, instead of an empty field and a "group … not found" error on Import or Save.
- Import from ~/.ssh: an `IdentityFile` with only a public key now warns that keys held by another agent are not supported, instead of saying such keys come in a later version.
- Import from ~/.ssh warns about a line such as `HostName a b` or `Port 22 x` (extra arguments, which ssh refuses) and skips it, instead of quietly taking the first value.

## 26.10.18 build 4

### Added

- Several windows: Shell ▸ New Window (⇧⌘N) opens another window with its own tabs, which can be moved to another display. A window's title follows the view in front: the tab in front, or Hosts on the Hosts view (TermPort whenever the vault is not unlocked: on the lock screen, the first-run setup screen and the vault-unavailable screen). While an SSH question (a host key, a password, a one-time code and the like) waits for your answer in a tab behind or while the window is not in front (another TermPort window or another app is), the window's title ends with "— waiting for input", so the Window menu shows which window asks; once you have answered and TermPort is waiting for the server, the suffix goes away. Menu commands and shortcuts act on the window in front; while a file sheet is open or the windows are minimized, they go to the window that was last in front, and a minimized window is restored first, except for Close Tab and the Edit menu commands (Select All, Find, Find Next, Find Previous, Clear Scrollback). Unlocking, locking or resetting the vault applies to all windows; a reset in another window also clears what was typed on this window's lock screen and closes its Reset dialog. The Quit TermPort button on the vault-unavailable screen quits the app, not only that window. Changes made in Settings (⌘,) apply to the other windows; the font size changed with ⌘=, ⌘− and ⌘0 stays per window. Closing a window ends its sessions; ⌘W on the Hosts view of a window with no tabs closes that window when it is not the only TermPort window, the first window too. Only the first window's size and position are remembered.
- TermPort app icon and logo (a green `>_` prompt on black) in place of the Tauri template ones.

### Changed

- TermPort requires macOS 13.3 or later (the interface relies on WebKit features older macOS versions lack).
- Long lists (Known Hosts, the import preview) render only the visible rows, so a known_hosts with thousands of lines stays responsive.
- Known Hosts rows have a fixed height: a key's comment now sits on the hosts line, and a long one is cut off with an ellipsis; hover to see the full text.
- The host editor says why Save is unavailable once the Address has been edited or when editing a saved host: "Address is empty" or "Address must not contain spaces" under Address; the group editor shows "Name is empty" under Name in the same cases.
- While a key is being generated, imported or renamed, or its saved passphrase is changed, the key sheet stays open: Cancel is disabled and Escape and ⌘W do nothing, so closing it no longer looks like cancelling a change that is still written.
- Importing a very large `~/.ssh/config` is much faster.
- Deleting a group says which of its own settings (username, port, password, keys, jump hosts, keepalive) stop applying to the hosts and groups that move out.

### Fixed

- Import from ~/.ssh reads `Match` criteria written as `host=a` or `!user=a,b`, as OpenSSH 10 does, instead of skipping the whole block; a block whose list is empty or starts with `#` is skipped with a warning.
- Import from ~/.ssh does not import a host whose `HostName` has an unknown `%` token (OpenSSH refuses such a host too); before, it was imported with an unusable address. Its other options (keys, known-hosts files, proxy) are not read either.
- Coming back to an open password card, host editor or dialog (after Settings, About or a tab switch) puts focus back in the field you left (if you left a button, on what gets focus when the card or dialog opens, for example the Password field of a password card or Retry on an error card), without selecting its text, so the next keystroke no longer replaces what you typed.
- The passphrase field of the key sheet gets focus again after "Wrong passphrase" or when a key turns out to need a passphrase.
- Import from ~/.ssh reports a `ProxyJump` with quotes, `\`, `$`, backticks or shell operators (for example `ProxyJump "a,b"` or `ProxyJump $GW`) as an invalid jump host list and keeps it in Notes; before, a jump host with those characters in its name was created.
- Saving a host or group whose jump host was created by a newer TermPort version no longer fails with "host … not found"; the link is kept, and loops and the 8-hop limit are still checked, counting that host as one hop.
- Deleting a record or clearing a saved secret no longer leaves the old encrypted copy in the vault's WAL file while TermPort runs.
- A `ProxyJump` in `~/.ssh/config` with an `ssh://` user that percent-decodes to a quote, `\`, `$`, a backtick, a shell operator or a space is now rejected like the same characters written directly.
- Public-key login with an RSA key whose size is not a multiple of 64 bits (for example 2049) no longer fails: the signature had extra leading zero bytes, which OpenSSH rejects.
- `scripts/version.sh` also updates the workspace versions in `Cargo.lock`.
- Reset TermPort closes every open session, local shells and SSH alike, before it deletes the vault, and the Reset dialog says so. Before, sessions left open behind the lock screen took input again once a new master password was set after the reset, so anyone at the computer could get them back without the master password.
- When keepalive is on (the default), an SSH session ends with "timed out while waiting for the server" once the server has accepted no data for four keepalive intervals (2 minutes at the default 30 s), instead of hanging during a large paste. With Keepalive 0 there is no such timeout.
- When a jump host drops the connection, the reason shown is the jump host's own (for example its disconnect message), not "connection lost".
- Saving a host or group is refused when it would make another host's jump route longer than allowed; the error names that host.
- An inherited Jump hosts list is shown, and copied by Override, only up to the host being edited, as the route uses it: a host no longer appears as its own jump host (for example, the bastion of a group shows None).
- Import: each unsupported option in a host's Notes names the file and line it really comes from; unsupported options from `/etc/ssh/ssh_config` are shown once as an import warning instead of in every host's Notes.
- On servers that ask for the password through keyboard-interactive, a wrong or out-of-date saved password, or a typo, no longer ends the login: TermPort asks again, up to 3 typed passwords per hop, shared with the password method. Once they are used up, the login fails at once.
- On keyboard-interactive, a wrong answer to another question (for example a one-time code) no longer ends the login: the server asks again, up to 4 tries per step.
- One-time code prompts (for example "One-time password (OATH)") are no longer taken for the login password or for a password change, whether they come before or after the password: the saved password is never sent to them, and the login password can still be remembered.
- Import: `Host` patterns in `~/.ssh/config` match case-sensitively, as in OpenSSH, so `Host Web` and `Host web` are separate hosts; `Match host` still ignores case.
- Import: `%`-tokens and `${VAR}` in `User` are expanded as OpenSSH does; a value that cannot be expanded is skipped with a warning instead of becoming the login name as written.
- Import: an `@revoked` line of `known_hosts` is imported even when the same host and key are stored as trusted, so a key revoked in `~/.ssh` is refused by TermPort too.
- In the host and group editors and the key sheet, Escape and Tab keep working after Reset to inherited, Override, a chip ×, password Clear/Undo or Remove file: focus moves to the next control instead of being lost.
- The Import from ~/.ssh dialog cannot be closed while an import is being written: Cancel is disabled and Escape and ⌘W are ignored until it finishes.
- When the connection drops while a question waits for you (a host key, a key passphrase, a username, a password or a keyboard-interactive question such as a one-time code), the question closes and the error reads "the connection closed while waiting for your answer" (before: "server closed the connection while waiting for confirmation"); keyboard-interactive questions now close at once instead of staying open until answered.
- Password-change prompts (new, retype, current, old password and the like) are never answered with the saved password; they are always shown to you, even right after a one-time code.
- Import: `ProxyJump none` no longer hides a later `ProxyCommand` (for example one in `Host *`), as in OpenSSH.
- Import: a host whose config ends with no jump host (`ProxyJump none` with no later `ProxyCommand`, `ProxyCommand none`, or a `ProxyCommand` that is not turned into a jump host) connects directly instead of through the jump hosts of the group it is imported into.
- Import: a `ProxyCommand` that runs a jump (for example `ssh -W %h:%p bastion`) and ends with a shell comment is turned into a jump host like one without the comment; one with shell operators, `$`, backticks or unusual whitespace is kept as written instead of becoming a broken jump host (for example `ssh -W %h:%p $BASTION` no longer becomes a jump host named `$BASTION`).
- Import: importing into a new group no longer creates an empty group when no host lands in it.
- Import: `known_hosts` lines whose key cannot be read are skipped with a warning instead of being imported and later causing a false "host key changed" warning.
- ⌘F no longer moves focus out of an open editor, key sheet or import dialog, or switches the pane behind it.
- After deleting a key or a saved host key, focus moves to the next row instead of being lost.
- Deleting the last host or group in a list no longer loses keyboard focus: it moves to the empty view's button or to the search field.
- Reconnect on a local terminal tab keeps focus in the terminal, so you can type at once.
- When the window regains focus, the lock screen keeps the field you were typing in (for example Confirm when creating a master password) instead of moving back to the first field.
- The passphrase sheet no longer asks for a "New passphrase": for a key with a saved passphrase it says that only the key's current passphrase is accepted and the key file is not re-encrypted.
- The Import button reads "Scanning…" during a rescan instead of "Importing…".
- Import: if the scan run again after an expired import fails, its error is shown, the old preview is cleared and focus stays in the dialog.
- Unlocking an encrypted key with a slow key derivation no longer ends in a "timed out while authenticating" error when the passphrase is right.
- Import no longer stores hosts whose first ProxyJump hosts lead back in a loop (for example `a` via `b` and `b` via `a`): the preview warns "jump hosts form a loop", and those hosts and every host that jumps through them are skipped. A later jump host in a ProxyJump list may still name a host already in the route.
- Enter and Escape that confirm or cancel an input method composition no longer act on their own anywhere: they do not move to the next match or close the find bar, connect or clear the search in Hosts, clear the Known Hosts search, answer a question card or close a dialog, editor or error card. On macOS this also covers the key that ends the composition.
- While a key import, a passphrase save or a config import is running, the passphrase field, the "Save passphrase in vault" box, the import checkboxes, All/None and the new group name are disabled, so changes that would be ignored can no longer be made.
- Enter or Space typed ahead no longer presses Retry the moment a connection error card appears.
- The same guard now also covers switching to a tab that shows an error card, a prompt card or the bar shown after the session ends ("Exited with code N", "Disconnected: …" or "Process exited"): Enter or Space pressed right after the switch no longer presses Retry, Reconnect, Save as Host, Close or "Add and Connect".
- A held Enter or Space never presses a button on a connection error card, a question card or the bar shown after the session ends, however long it is held: for example, Enter held in the terminal no longer presses Reconnect when the session drops. A held Escape closes one card, dialog or drawer, not the next ones behind it, and does not reach the terminal or search field that gets focus after it.
- `Match !final` and `Match !canonical` blocks in the SSH config are now applied on import, as OpenSSH does, instead of being skipped with a "not evaluated" warning.
- Unlocking the vault restarts the same guard for the card or bar of the tab in front, so Enter or Space typed right after unlocking no longer presses one of its buttons.
- An editor with a Port or Keepalive value that is not valid now asks "Discard changes?" before closing instead of dropping the typed value.
- Deleting a saved host key no longer promises a prompt on the next connection: for an ordinary entry it says TermPort will ask before trusting the key again; for a revoked entry it says only that deleting it lifts the revocation.
- Password-change prompts from the server (current password, new password) are shown as the server's own questions instead of repeated "wrong password" cards, and no password is saved after such a change.
- When a server does not answer the password in time (it may be slow, unreachable, or require a password change), the connection fails with an error that says so instead of a plain timeout.
- A key whose private part does not match its stored public key is skipped with a notice saying so, instead of a bare authentication failure.
- Import: a slower, older scan of `~/.ssh` can no longer replace the result of a newer one.
- When, while TermPort is unlocked, the vault file is overwritten in place from outside TermPort (for example restored from a copy with another master password, or overwritten with another vault), TermPort locks as with Lock and shows the lock screen the next time it reads or saves the vault, instead of staying open and failing every action with "vault is damaged". If the vault file is instead replaced by a new file (renamed over, moved or deleted), TermPort reports the vault as unavailable and offers only Quit until it is restarted.
- In the host and group editors, after Change on a saved password, an empty field shows "keeps the saved password", which is what Save does, also when no password is inherited from a group; before, it showed "from group …" or no hint.
- The ⋯ button of a Known Hosts row is announced to VoiceOver as "More actions for …", as it only opens a menu.
- When Change Master Password fails for a reason other than a wrong current password (for example the vault cannot be written), focus returns to the Current field instead of being lost.
- View ▸ Bigger and Smaller (⌘= and ⌘−) no longer need extra presses to come back after the font size has reached its limit: the first press the other way changes the size.
- Import: when an encrypted key's `.pub` file claims the fingerprint of a key in `~/.ssh` that can be checked from its private part, only the checked key is imported, if it is selected; the encrypted key is skipped even when it alone is selected, and the import preview warns about it ("its .pub matches <file>; the encrypted key was not checked against it and is not imported"). A key already stored in the vault keeps its id when imported again, so an encrypted key imported earlier from a mismatched `.pub` stays as it is: delete it in Keys before importing again.
- A dialog underneath another one no longer takes keyboard focus from it: neither when it opens, nor when an import scan or key import finishes in the background, nor when it moves focus back to its field after an error; when Settings or About closes over the lock screen, the Reset dialog gets keyboard focus back.
- The key sheet and the Import from ~/.ssh dialog keep keyboard focus after an error instead of losing it; after a failed save in the host or group editor, keyboard focus returns to the form.
- When Reset TermPort fails, typing goes back to the RESET field.
- A window no longer shows itself unlocked when the vault was locked again a moment after unlocking.
- Pasting `user@host:port` into the host editor's Address field replaces it with the parsed address (and fills in the username and port) only when the field is empty or fully selected; otherwise the text is pasted as usual.
- After you answer an SSH question, the tab shows a spinner while TermPort waits for the server, instead of the dot that means a question waits for you.
- Holding ⌘D on the Hosts view no longer makes a chain of copies: it duplicates the host once. Holding Enter in the host list or the search field no longer opens groups and hosts one after another: it opens the group or connects the host once. After Duplicate, the selection and keyboard focus move to the copy instead of briefly jumping to the first row.
- An address copied with Copy Address (such as `[web]:2222`) can now be used for quick connect in the Hosts search, in the Known Hosts search and when pasted into Address.
- A keyboard-interactive login that waits on a second factor, such as a push approval on the phone, now has up to 2 minutes after each answer, such as the password or a one-time code, instead of 30 seconds; when the server stays silent, the error says it may be waiting on a second factor.
- A new vault no longer leaves its first write in `vault.db-wal`.
- With regex search on and an invalid pattern (such as `(`), Enter, ⇧Enter, the ‹ › buttons and ⌘G/⇧⌘G in the find bar no longer raise an error; the bar keeps showing No results.
- Closing Settings, About or Change Master Password while the find bar is open returns the cursor to the find field (without selecting its text); before, typed keys went nowhere until you clicked.
- Import: a jump host written with a user or port in `ProxyJump` (for example `ProxyJump bob@bastion`), or one whose name only a `Host` pattern matches, keeps its `HostKeyAlias` and `ServerAliveInterval`; before, its host key was checked under the wrong name and the default keepalive was used.
- When saving a changed host key or importing from `~/.ssh` fails while writing the vault (for example the disk is full), nothing is saved; before, the old host key could be deleted without the new one being saved, or the hosts imported without their host keys.

## 26.10.16 build 3

Stage 2: SSH basics.

### Added
- **SSH sessions in tabs.** A host opens in its own tab. While it connects, a card shows the step (connecting, exchanging keys, authenticating, starting the shell) and a Cancel button. On an error the card offers Retry and Close, and Edit Host for a saved host. When the remote shell exits with code 0 the tab closes; otherwise a bar shows the exit code or "Disconnected: <reason>" with Reconnect and Close. Tab context menu: Reconnect, Duplicate, Edit Host (Save as Host… for a quick-connect tab), Close. Tab marks: a spinner while connecting, a dot while a question waits for you, red on error, grey after the session ends.
- **Hosts and groups.** The Hosts view (⌘1 or ⇧⌘H) lists groups and hosts with breadcrumbs. Search finds hosts in all groups. Keyboard: arrows, Enter connects or opens a group, ⌘I edits, ⌘D duplicates, ⌘⌫ deletes, ⌘↑ goes to the parent group; also double-click and context menus. Shell ▸ New Host… (⌘N) opens the host editor in the current group from any view. Groups nest; a host takes username, port, password, keys, jump hosts and keepalive from its groups unless it sets its own. The editor shows where each inherited value comes from, with Override and Reset to inherited.
- **Jump hosts:** chains of up to 8 hops including the target, built by TermPort itself without an external `ssh`. Host cards and the editor show the route ("via bastion").
- **Authentication:** keys from the vault (the passphrase is asked only after the server accepts the key), keyboard-interactive and password. A password can be saved on a host or on a group; the prompt says where it will be saved. When no username is set, TermPort asks for one.
- **Quick connect:** type `user@host:port` in the search field and press Enter. It offers no keys (none from the vault, from `ssh-agent` or from the key files in `~/.ssh`): it signs in with keyboard-interactive or a password and saves only the host key. "Save as Host" (on the bar after the session ends or in the tab's context menu) opens the host editor with the address, and the port and username if you typed them, filled in; pick a key there to sign in with it.
- **Known hosts** in the vault. An unknown key asks Cancel / Add and Connect. A changed key shows a red warning: Cancel is the default, and Replace and Connect works only with a click. `@revoked` keys are refused. The Known Hosts pane lists, searches and deletes saved keys.
- **Keys:** import by paste, file picker or drag and drop; generate Ed25519, ECDSA P-256 or RSA 4096; rename; save or clear the passphrase stored in the vault (the key itself is not re-encrypted); copy the public key; delete.
- **Import from ~/.ssh** (Shell → Import from ~/.ssh…): hosts from `config` (with `Include` and the `Match` blocks that can be decided without running commands), private keys and `known_hosts`. A preview lets you pick what to import and into which group. Files in ~/.ssh are only read.
- **Encrypted vault with a master password** (at least 8 characters). Hosts, groups, keys, passwords and known hosts are stored encrypted. Lock Vault: ⇧⌘L. Change Master Password… re-encrypts the vault with a new key. "Forgot password? Reset TermPort…" deletes the vault after you type RESET; files in ~/.ssh are not changed.
- **Lock:** while locked the window shows only the lock screen. Running sessions keep going, but typing into them is blocked until you unlock.
- **Delete confirmations** for hosts, groups, keys and known hosts say what else is affected (for a key: how many hosts and groups use it). Empty lists show what to do next.
- **Edit menu: Undo, Redo and Cut** for text fields.

### Changed
- **TermPort opens on the Hosts view after unlock.** ⌘T still opens a local terminal, but only once the vault is unlocked (Touch ID unlock comes in stage 3).
- **⌘1 is Hosts;** ⌘2…⌘8 switch to terminal tabs 1…7, ⌘9 to the last one.
- **Stricter content security policy** for the window.
- **No leading zeros in the version date:** `27.1.6 build 40`, not `27.01.06 build 40`; the same in git tags (`v27.1.6.build.40`). About TermPort shows the version this way too.

### Fixed
- **`scripts/version.sh set` with an invalid version no longer writes garbage** into `Cargo.toml` and `package.json`; it stops with an error and changes nothing.
- **Closing a local tab while its shell prints a lot of output (for example `yes` or `cat` of a large file) now ends the shell.** In 26.10.15 build 2 the shell and the running command stayed behind until TermPort quit.

## 26.10.15 build 2

Stage 1: local terminal.

### Added
- **Local terminal in tabs.** Each tab runs your login shell on the computer. New tab: ⌘T or the + button; close: ⌘W or a middle click; switch: ⌘1…⌘9 (⌘9 is the last tab), ⌃Tab / ⌃⇧Tab, ⇧⌘[ / ⇧⌘]. The tab title follows the terminal title; a dot marks new output in a background tab. When the shell exits normally the tab closes; otherwise it stays open and shows the exit code.
- **Themes, Homebrew by default** (green on black), plus System (follows the macOS appearance), Light, Dark, Solarized Light and Solarized Dark. The tab bar and the rest of the window follow the theme colors.
- **Settings (⌘,):** theme, font, size, line height, cursor shape and blinking, scrollback length, Option as Meta. Only changed values are stored, so a new default reaches every setting you never touched.
- **Font size from the keyboard:** ⌘= bigger, ⌘− smaller, ⌘0 actual size.
- **Search in the terminal (⌘F):** next and previous match with Enter / ⇧Enter or ⌘G / ⇧⌘G, match case, regular expressions, match counter.
- **Copy and paste:** ⌘C, ⌘V, Select All (⌘A), Clear Scrollback (⌘K), and the same in the right-click menu.
- **Drag and drop:** files dropped from Finder are pasted as shell-quoted paths.
- **Links:** ⌘-click opens a URL in the browser.
- **The window remembers its size and position**, and whether it was maximized or in full screen.
- **About TermPort** shows the version.
- **Flow control:** when a command prints a lot, the shell waits until the terminal has drawn the output.

### Changed
- **Version format is `YY.MM.DD build N`** (was `YY.MM.DD-N`). N grows by one with every build and never resets, also across days. Git tags: `vYY.MM.DD.build.N`.

## 26.10.15 build 1

Stage 0: skeleton.

### Added
- Cargo workspace; a Tauri 2 + Svelte app that opens a window.
- `scripts/version.sh` and a local macOS build (`scripts/build-mac.sh`): ad-hoc signed `.app` and `.dmg`.
