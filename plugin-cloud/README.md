# Peka for every computer with your Claude login

Add this on claude.ai instead of `peka`, not as well as it, and press Connect on its Connectors tab. Each computer with your Claude login then joins your peka account by itself after its first reply in Claude Code. In the desktop app's Code tab, run `/peka-cloud:login` once instead.

Point at something in your browser, say what should change, and your Claude Code session gets the note, with everything it needs to find the code.

To install Peka, copy the setup prompt from https://getpeka.com/install and paste it into Claude Code. The same page has the steps to do it by hand.

## What this plugin runs, sends and fetches

- `runtime/peka` is a compiled program. It starts with each session as its MCP server, and after each of Claude's replies to wait for notes. It talks to Peka's hub on this computer, at 127.0.0.1.
- With Peka cloud, it also talks to `https://hub.getpeka.com`, which then holds your notes and their screenshots, session titles and first prompts, and this computer's name.
- `peka setup` runs only when you run it. It downloads Peka's hub from https://downloads.getpeka.com, checks it against the checksum in `runtime/setup.json`, puts it in `~/.peka`, and starts it. It also asks Chrome to add Peka's extension from the Chrome Web Store, through a per-user registry entry on Windows or a file on macOS, and Chrome asks you to enable it. With `--cloud` it skips the hub and opens getpeka.com for you to approve this computer.
- `/peka-cloud:login` connects this computer to your peka account, in your browser.
- After each reply, until this computer has joined, the plugin sends peka cloud a hash of a token it made and a hash of the session's id. The peka connector, at `https://hub.getpeka.com/mcp`, vouches for that session.
