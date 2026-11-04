---
description: Install peka's hub on this computer, so notes stay here (the free version)
---

Install peka's hub on this computer by running its setup program with the Bash tool:

"${CLAUDE_PLUGIN_ROOT}/runtime/peka" setup --local

On Windows, run "${CLAUDE_PLUGIN_ROOT}/runtime/peka.exe" setup --local instead.

It downloads the hub, about 30 MB, into ~/.peka and starts it. Notes then go from the user's browser to Claude Code sessions on this computer, and never leave it. Tell the user in a sentence or two what it printed and anything left for them to do. If they haven't added peka's Chrome extension yet, mention /peka:setup:chrome.
