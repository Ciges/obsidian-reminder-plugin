# Obsidian Reminder fork

Original Obsidian Reminder version: **1.3.2**
Fork version: **1.3.2.2**

Local fork of the [Obsidian Reminder](https://github.com/uphy/obsidian-reminder) plugin (built files, not source code) to create a custom version. Made by modifying the JavaScript code. The `main.js` has been de-minified to keep the customizations readable and maintainable across upstream updates. Original authorship (`uphy`) is preserved in `manifest.json`.

## Customizations

All changes live in `main.js` (and `styles.css` for the last one), marked with a `// Fork Ciges` comment.

Changes 1 and 2 adapt the plugin to a workflow that uses custom task-checkbox states:

1. **Extra statuses treated as completed** — `checkedStatuses` extended from `["x", "-"]` to `["x", "-", "p", "d", ">"]`. This stops reminders from firing on tasks already finished as:
   - `[p]` — done correctly
   - `[d]` — discarded
   - `[>]` — delegated
   - (`[-]` "unnecessary" was already in the original)
2. **"Done" button marks `[p]`** — `setChecked` changed so the reminder's "Done" button sets the task to `[p]` instead of `[x]` (`this.check = e ? "p" : " "`).

Change 3 is a new feature:

3. **"Show note name in reminder list" setting** — new boolean option under *Settings → Reminder → Display* (default **on**, preserving the original behavior). When turned **off**, the source note name next to each reminder is hidden in the reminder list view. Implemented without touching the compiled Svelte render: the view toggles a `reminder-hide-note-name` CSS class on its container (reactively, via the setting's `onChanged`), and a rule in `styles.css` hides `.reminder-file` for that state. Only the sidebar reminder **list** is affected; the notification popup/toast still shows the note name.
