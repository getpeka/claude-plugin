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
- **With Peka cloud, for notes between your computers:** run `/peka:setup:cloud` on each one, and approve it in your browser. With the Peka connector added to your Claude account, from Claude's directory, a computer with this plugin asks to join by itself after its first reply.
- `/peka:status` says how Peka is set up here.

Step by step: <https://getpeka.com/docs>

## What this plugin runs, sends and fetches

- `runtime/peka` is a compiled program, Peka's session client: `peka.exe` on Windows, and on macOS the `runtime/peka` launcher, which picks the build for the computer. Claude Code starts it with each session as an MCP server, which gives Claude `list_feedback`, `get_feedback` and `update_feedback`, and after each of Claude's replies as a Stop hook that waits for notes and wakes the session. It talks to Peka's hub on this computer at 127.0.0.1 and, with Peka cloud, to https://hub.getpeka.com.
- So that your browser's session menu can show a session, it reads the session's title, the start of its first prompt, and when it was last used from Claude Code's transcript and session files on this computer. With Peka cloud the title and prompt are encrypted for your browsers before they leave this computer.
- A note it fetches holds what you captured: your comment, screenshots, page details and console output. With Peka cloud, notes are end-to-end encrypted, and this computer can open only the notes sent to its own sessions.
- When a note arrives while the session is idle, the session client posts it into the session's own inbox, which Claude Code gives it. It reads Claude Code's settings to see whether that inbox takes messages.
- `.mcp.json` also lists the Peka connector, at https://hub.getpeka.com/mcp. It does nothing until you connect it, and Claude Code shows it as needing sign-in until then.
- On a computer that isn't connected to Peka cloud, and only if your Claude login has the Peka connector (Claude Code lists the claude.ai connectors it has connected in its settings file, `.claude.json`), the Stop hook asks Claude, at most once a week, to connect this computer by calling the connector's `peka_connect_computer` tool with a hash of a token this computer made. The token stays in `~/.peka`.
- A PostToolUse hook reads that tool's answer on this computer before Claude sees it. It finishes connecting this computer, sending the token, the key in the answer and this computer's public key to https://hub.getpeka.com, or it cancels a connection this computer didn't start. Claude never sees the key.
- `/peka:setup:cloud`'s hook (`peka login`, which `/peka:login` also runs) asks https://hub.getpeka.com for a code, and gives Claude the hash to pass to the connector and a link to approve this computer on getpeka.com, for when Claude has no connector.
- `/peka:setup:local` runs `runtime/peka setup --local`, only when you run it. It downloads Peka's hub from https://downloads.getpeka.com, checks it against the checksum in `runtime/setup.json`, puts it in `~/.peka`, and starts it.
- `/peka:setup:chrome` runs `runtime/peka setup --chrome`, only when you run it. It asks Chrome to add Peka's extension from the Chrome Web Store, through a per-user registry entry on Windows or a file on macOS, and Chrome asks you to enable it.
- `/peka:status` runs `runtime/peka status`, which reads what's set up here and changes nothing. With a key waiting to join, it asks https://hub.getpeka.com how that join stands.

## Privacy and support

- What Peka keeps, and for how long: <https://getpeka.com/privacy>
- Questions: hello@getpeka.com
