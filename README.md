# Peka

Point at something in your app in Chrome, say what should change, and the note reaches your Claude Code session with a screenshot, the element's selector and HTML, the component behind it and the page's console errors. Claude makes the change and tells you in the browser what it did, or asks you there. A note wakes the session even when it's idle.

## Set up

Copy the setup prompt from <https://getpeka.com/install> and paste it into Claude Code on each computer. Claude installs this plugin, sets up the computer, and adds the Peka extension to Chrome. The same prompt updates it later.

By hand, in Claude Code:

```
/plugin marketplace add getpeka/claude-plugin
/plugin install peka@getpeka
```

- **On this computer only, for free:** run `/peka:setup:local` and `/peka:setup:chrome`. They install Peka's hub here and add the Chrome extension, and notes never leave this computer.
- **With Peka cloud, part of Pro, for notes between your computers:** run `/peka:setup:cloud` on each one, and approve it in your browser, where the page shows the same code Claude gives you.
- `/peka:status` says how Peka is set up here.
- **Updates:** setting up turns on Claude Code's automatic updates for Peka, so a new version arrives by itself and takes effect in your next session. `/peka:update` updates it now, and Claude says when a newer Peka is out.

Step by step: <https://getpeka.com/docs>

## What this plugin runs, sends and fetches

- `runtime/peka` is a compiled program, Peka's session client: `peka.exe` on Windows, and on macOS the `runtime/peka` launcher, which picks the build for the computer. Claude Code starts it with each session as an MCP server, which gives Claude `list_feedback`, `get_feedback` and `update_feedback`, and after each of Claude's replies as a Stop hook that waits for notes and wakes the session. It talks to Peka's hub on this computer at 127.0.0.1 and, with Peka cloud, to https://hub.getpeka.com.
- So that your browser's session menu can show a session, it reads the session's title, the start of its first prompt, and when it was last used from Claude Code's transcript and session files on this computer. With Peka cloud the title and prompt are encrypted for your browsers before they leave this computer.
- A note it fetches holds what you captured: your comment, screenshots, page details and console output. With Peka cloud, notes are end-to-end encrypted, and this computer can open only the notes sent to its own sessions.
- When a note arrives while the session is idle, the session client posts it into the session's own inbox, which Claude Code gives it. It reads Claude Code's settings to see whether that inbox takes messages.
- `/peka:setup:cloud` (and `/peka:login`, the same) runs `runtime/peka setup --cloud`, only when you run it. It makes a token that stays in `~/.peka`, asks https://hub.getpeka.com for a code, and opens your browser on getpeka.com to approve this computer with it. Once you do, it sends this computer's public key there, and the computer is in your account.
- `/peka:setup:local` runs `runtime/peka setup --local`, only when you run it. It downloads Peka's hub from https://downloads.getpeka.com, checks it against the checksum in `runtime/setup.json`, puts it in `~/.peka`, and starts it.
- `/peka:setup:chrome` runs `runtime/peka setup --chrome`, only when you run it. It asks Chrome to add Peka's extension from the Chrome Web Store, through a per-user registry entry on Windows or a file on macOS, and Chrome asks you to enable it.
- Running `runtime/peka setup` with any of those also turns on Claude Code's automatic updates for this plugin's marketplace: it sets `autoUpdate` to true on the marketplace's `extraKnownMarketplaces` entry in Claude Code's user settings (`~/.claude/settings.json`), as the toggle in `/plugin` does. If you turned them off there, it leaves them off.
- Once a day the MCP server asks https://getpeka.com/api/plugin which version of Peka is newest, in a process of its own, and keeps the answer in `~/.peka/latest.json`. When this copy is older, Claude reads that in its instructions at the start of the next session. The request carries nothing about you or your notes. If `/peka:setup:local` installed Peka's hub and this plugin names a newer hub in `runtime/setup.json`, the same process downloads it from https://downloads.getpeka.com and checks its checksum, and it starts when the hub next does. `PEKA_NO_UPDATE_CHECK=1` turns both off.
- `/peka:update` runs `runtime/peka update`, only when you run it. It runs Claude Code's own `claude plugin marketplace update` and `claude plugin update` for this plugin, then the new version's `peka update --finish`, which turns on automatic updates as above and updates the hub, restarting it if it's running.
- `/peka:status` runs `runtime/peka status`, which reads what's set up here and asks https://getpeka.com/api/plugin which version is newest. It keeps that answer, as the daily check does, and changes nothing else.

## Privacy and support

- What Peka keeps, and for how long: <https://getpeka.com/privacy>
- Questions: hello@getpeka.com
