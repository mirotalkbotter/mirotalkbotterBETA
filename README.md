# MiroTalk Bot Panel

A small local control panel that sends bots into a [MiroTalk P2P](https://p2p.mirotalk.com/) room.

Type a room name, press **Enter**, and the panel opens a local Chrome/Edge browser, joins
`https://p2p.mirotalk.com/join/<room>` over and over and gives every bot a name: `wtv1`, `wtv2`, `wtv3` …

## Run it

Double-click **`start.bat`** (or run `node server.js`), then open <http://127.0.0.1:3000>.

First run installs `puppeteer-core` via npm.

## Controls

| Control | What it does |
|---|---|
| Room name box + **Enter** | Starts joining that room |
| **Start joining** | Same thing as pressing Enter |
| **Stop** | Stops new bots from joining. Bots already in the room stay. |
| **Disconnect all** | Kicks every bot out of the room (and stops spawning) |
| **✕** on a bot card | Disconnects just that bot |
| Number of bots | `0` = keep joining forever until you press Stop |
| Delay between joins | Pause between two joins (ms) |
| Name prefix | `wtv` → `wtv1`, `wtv2`, … |
| Hide bot windows | Headless mode (off = you can watch the bot windows) |

## How it works

- `server.js` – local HTTP server + JSON API on `127.0.0.1:3000`
- `bots.js` – bot engine: launches Chrome/Edge through `puppeteer-core`, one isolated
  browser context per bot, fills the "Display name" field and clicks **Join meeting**
- `public/index.html` – the dashboard

Bots run with `--use-fake-device-for-media-stream`, so they use a **virtual camera/microphone**
— your real camera and mic are never opened. Maximum 16 live bots at once (MiroTalk P2P is
peer-to-peer, so every bot connects to every other participant).

## Notes

- Use it only on rooms you own or have permission to test.
- Rooms that are password protected or locked will show up as an error in the log.
- If no Chrome/Edge is found, install one or set `BOT_BROWSER_PATH` to your browser's `.exe`.




