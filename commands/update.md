---
description: Update Peka to its newest version, with Claude Code's own plugin commands
---

Update Peka by running its update program with the Bash tool:

"${CLAUDE_PLUGIN_ROOT}/runtime/peka" update

On Windows, run "${CLAUDE_PLUGIN_ROOT}/runtime/peka.exe" update instead.

It runs Claude Code's own `claude plugin marketplace update` and `claude plugin update` for Peka's marketplace, then the new version finishes by itself: it turns on Claude Code's automatic updates for Peka, unless the user turned them off, and updates Peka's hub on this computer if it has one. It can take a minute.

Tell the user in a sentence or two what it printed. A new version takes effect in a new session, or in this one after the user runs /reload-plugins, which you can't run for them.

If it says `claude` didn't work, run the same two commands yourself, with "$CLAUDE_CODE_EXECPATH" in place of claude if claude isn't found: claude plugin marketplace update getpeka, then claude plugin update peka@getpeka.
