# 3ds-rpc-icons

Public icon mirror for the **DiscordNowPlaying** 3DS → Discord Rich Presence
bridge (`/mnt/Parity/projects/3dsStuff/DiscordNowPlaying` on Mirai).

Discord resolves Rich Presence images **server-side**, so `large_image` has to
be a publicly reachable URL — a LAN address (`http://192.168.1.174:8080/...`)
renders as a grey placeholder in other people's clients. The daemon on Mirai
serves its icon cache at `<daemon_public_base_url>/icons/<titleid>.png`, and
that base is pointed here:

    daemon_public_base_url=https://raw.githubusercontent.com/KiyomiLovesOreos/3ds-rpc-icons/main

So `large_image` becomes
`https://raw.githubusercontent.com/KiyomiLovesOreos/3ds-rpc-icons/main/icons/<TITLEID>.png`.

## Contents

`icons/<TITLEID>.png` — 48x48 RGB565 SMDH icons, unpacked from the 3DS (PICA200
morton-swizzle undone) and re-encoded as PNG. Filenames are the exact uppercase
16-hex title id the console reports, so the path is reproducible.

## Keeping it in sync

New game → the 3DS uploads its icon to the daemon on title change → the icon
lands in `~/.config/discord-now-playing/icons/`. Publish it with:

    /mnt/Parity/projects/3dsStuff/DiscordNowPlaying/sync_icons.sh

`discord-icons-sync.timer` runs the same script every 10 minutes.

Until a title id is present here, that game's presence simply has no large
image (Discord shows the app placeholder instead of a broken/white image).
