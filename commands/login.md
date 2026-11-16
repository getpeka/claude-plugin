---
description: The same as /peka:setup:cloud: connect this computer to your Peka account
---

Connect this computer to the user's Peka account by running its setup program with the Bash tool, in the background, because it waits while the user approves the computer:

"${CLAUDE_PLUGIN_ROOT}/runtime/peka" setup --cloud

On Windows, run "${CLAUDE_PLUGIN_ROOT}/runtime/peka.exe" setup --cloud instead.

It opens the user's browser on Peka's page for this computer, and prints a link and a code. Tell the user both as soon as they appear: they check that the page shows the same code, and press Connect. When it says the computer is connected, tell them in one sentence.
