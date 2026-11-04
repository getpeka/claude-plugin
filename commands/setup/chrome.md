---
description: Add peka's extension to Chrome on this computer
---

Add peka's Chrome extension on this computer by running its setup program with the Bash tool:

"${CLAUDE_PLUGIN_ROOT}/runtime/peka" setup --chrome

On Windows, run "${CLAUDE_PLUGIN_ROOT}/runtime/peka.exe" setup --chrome instead.

It asks Chrome to add the extension from the Chrome Web Store, and Chrome asks the user to enable it the next time it starts. If Chrome is open, it opens the extension's store page instead, for the user to press Add to Chrome. Tell the user in a sentence or two what it printed and anything left for them to do.
