# Obsidian Reminder fork

Original Obsidian Reminder version: **1.3.2**
Fork version: **1.3.2.1**

Local fork of the [Obsidian Reminder](https://github.com/uphy/obsidian-reminder) plugin (built files, not source code) to create a custom version. Made by modifying the JavaScript code. The `main.js` has been de-minified to keep the customizations readable and maintainable across upstream updates. Original authorship (`uphy`) is preserved in `manifest.json`.

## Customizations

Both changes live in `main.js`, marked with a `// Fork Ciges:` comment, and adapt the plugin to a workflow that uses custom task-checkbox states:

1. **Extra statuses treated as completed** — `checkedStatuses` extended from `["x", "-"]` to `["x", "-", "p", "d", ">"]`. This stops reminders from firing on tasks already finished as:
   - `[p]` — done correctly
   - `[d]` — discarded
   - `[>]` — delegated
   - (`[-]` "unnecessary" was already in the original)
2. **"Done" button marks `[p]`** — `setChecked` changed so the reminder's "Done" button sets the task to `[p]` instead of `[x]` (`this.check = e ? "p" : " "`).

## Updating from upstream

When pulling a new upstream release, re-apply both changes: search for `setChecked` and `checkedStatuses` in `main.js`, then reproduce the two edits above (variable names may differ if the file is re-minified).
