# Changelog

> Only **user-visible changes** are listed, newest first. Versions match the tags on GitHub Releases.
> Earlier versions (v0.21.0 and before) are only recorded in Releases: https://github.com/hqweay/shunshou/releases

## v0.33.0

- **Transforms on variables, right inside templates.** Any template reference can now carry a transform
  pipeline — chained and composable: `{{title|trim|slice(0,20)}}` (trim, then cut to 20 characters),
  `{{selection|oneline}}` (collapse line breaks into one line), `{{page.images|count}}` (count the items),
  `{{title|default("N/A")}}` (fallback for an empty value). 19 are built in:
  trim / one line / quote prefix / case / slice by character / truncate / length / non-empty line count /
  split by separator / first and last line / join lines / regex replace / capture group / URL encode and
  decode / empty-value fallback / image list to Markdown.
  Transforms used to be available only on a "field source" (a fixed few, applied once while reading);
  now **the same variable can be transformed differently in each place** — tidy for a note, short for a
  message, encoded for a URL, without getting in each other's way.
  While writing a template, click the `|` next to a variable in the inserter to expand the transform chain
  (tick, fill in arguments, insert). A misspelled name or a bad argument is named in the diagnostics —
  **one typo will not** silently empty out a whole note.
- **Instagram image fetching on Safari (userscript) no longer comes back with "not a single image".**
  This path used to fail as a whole, leaving a single `[object Object]` in the log. The cause: it requested
  the public page over the extension channel carrying login state, so the site treated it as "not sent by
  the page itself" and returned only an empty shell. Such requests now go out with **the page's own
  identity** (no login state), and a failure now says whether it was the network, a login wall, or a
  changed page structure.
- **Image fetching is sturdier and dropped images are no longer silent.** A transient network failure is
  retried once (no more clicking "share" twice to get the full set); a temporary failure is no longer
  remembered as permanent (before, a few quick tries could keep coming up short until a minute had passed);
  an image that genuinely cannot be fetched no longer disappears quietly — the card says "N images could
  not be fetched".

## v0.32.0

- **Download Instagram originals in one click.** The Instagram scene gained "Download Instagram images": it
  fetches the post's original images (carousel auto-completed, up to 30) and shows them in the result dialog
  for one-by-one preview / copy / "Download all". **Nothing is saved to disk automatically** — what to keep is
  your call (to automate it, add a "Save as file" step after it in the action chain). Unlike the two "share"
  actions it does **no re-layout**: you get the post's own images. A Reel only has a cover image.
- **Instagram images come out complete, without profile pictures.** A second public source (the official embed
  page) is used as a fallback and the request headers are aligned (desktop + English is what returns the full
  data); the avatar filter no longer pins a CDN version segment, and thumbnails of other posts in
  recommendations are no longer pulled in. The userscript's image-domain allowlist was updated to match.
- **Translation stops lying.** "Downloading the language pack for the first time" used to flash even when the
  pack was already there (the translation appeared while it still said "downloading"). The notice now **only
  appears if there is a real wait (over 400ms)** and disappears the moment the model is ready; a genuine
  first-time download still shows progress.

## v0.31.0

- **Web highlights.** Select a passage, click "Highlight" on the capsule, and it stays on the page (through a reload,
  and after reopening) — **without changing the page's own structure**. Click a highlight again to "Copy this one"
  or "Remove this one" (removal can be undone). The highlights on a page can be saved to Orca / SiYuan in one go,
  copied as text, and previewed in the "Extract" page's "Variables on this page"; reference them in any template
  with `{{highlights}}`. Pages you set to "Do not run" are not involved. (On Safari a very large number of
  highlights can slow the page down — the cap is 200 per page.)
- **Config sync (Data page).** Moving between devices no longer means carrying your config by hand: use your own
  GitHub Gist as the storage. On one device click "Copy config and open a new Gist", on the other paste the
  address and "Fetch" → preview → "Apply to this device" (undoable); later changes can go back up with
  "Update the cloud copy". **Secrets are not synced** (after applying, it tells you exactly which keys this device
  is still missing), and **per-device** settings such as the orb position and onboarding are never overwritten.
  What sits in the cloud is plain text — use a secret Gist.
- **The Data page is easier to use, and a single action can be shared on its own.** Arriving here from "Export this
  scene" in a scene now expands it, generates the JSON, scrolls to it and highlights it — no hunting around.
  Node and group rows gained "Share…", so **one action** can be exported as an action pack and sent to someone;
  on import the destination is offered according to what the pack contains (a pack with just one action no longer
  asks you to "install it as a new scene"). Pasting someone else's pack and hitting "Parse preview" points out the
  parameters that are wrong (which action, which parameter name it does not recognize, or which value has the wrong
  type) and says the action will run with defaults and do nothing useful — these used to surface only after
  installing and actually running that step. The preview is a heads-up only — it does not block installing.
- **Action chains can be reordered as a whole, and nodes can move in and out of groups.** An action is no longer
  locked by "pick the main step first, then add the rest": steps are now a list whose first row is the main step, and
  the whole chain can be moved up and down (including swapping the main step further back), with cross-references
  inside the chain rewritten to follow. "Move to…" on an action row gained a "This scene" section, so an existing
  node can be moved into a group or back to the top level with its parameters, content scope and chain intact
  (previously you had to delete and rebuild it).
- **"Add action" was rebuilt.** It is now an in-panel picker: while searching, matches are **flattened into one list**
  (instead of staying inside their original groups for you to find again), opening it first offers "Recently used", and
  the "New from \"X\"" row is now emphasized. After picking, the new action **scrolls into view and flashes**, instead
  of being added out of sight.
- **Two AI config assistant improvements.** Generated variable groups finally have a **group name** (a group used to be
  called "Title", making it look like that was all it contained), and the AI page's two candidate rows are merged into
  one with **this page's candidates first** and the built-in examples after them — the same sentence is no longer said
  twice.
- **More accurate article clipping (general criteria, no allowlist).** The article container now uses a general set of
  criteria (visible text only, then the lowest common ancestor), so a page like a Douban group topic whose article is a
  single paragraph no longer falls back to the whole page; inline script JSON inside the page is no longer mistaken for
  article text and can no longer lure the model into picking a huge container.
- **"AI find the content scope" is revisitable.** Once candidates arrive the panel is no longer a one-shot: you can
  reopen it and keep looking, click another row to **switch in place** (no second model call, no extra cost), and
  "Ask again" is the explicitly-paid path. Candidates also come with two **free** ways to "see the effect": drawing the
  range on the page, and a content preview of "N characters taken · first 60".
- **Picking sessions are easier to finish.** Every "pick on the page" session now shares one exit contract — `Enter`
  finishes, `Esc` cancels, and the hint bar carries always-visible "Done / Cancel" buttons (**on a phone there used to
  be no exit at all but reloading the page**). The "Save as variable" dialog now **shows the value it just read**
  (telling "no match" and "read empty" apart), so you no longer have to write it into the config and run a trial
  calculation to find out.
- **Other fixes.** Links saved to notes drop tracking parameters (the general list grew past 150 names, and Weibo app
  share parameters are cleaned too); the Studio's collapsible headers are clickable across the whole row (not just the
  ▸); and the mode menu in a short panel is no longer clipped by the panel.

## v0.30.0

- **List pages can be read item by item now.** Comment threads, search results and timelines are repeating
  structures: previously you could only get the first item, or grab the whole block and end up with
  nicknames, timestamps and "1 reply" mixed in (which is where "the clip came with a pile of noise" usually
  comes from). Now you can read a repeating group item by item: pick sub-fields per item (author / time /
  body) and join them with your own per-item template, with a separator between items. The "Extract" page has
  an editor for it (container / per-item fields / per-item template / index / separator / item cap), and you
  can nest one level (replies inside comments). There is a cap (100 items by default) and when it is hit the
  output says "N more not taken" instead of dropping them silently. AI-generated actions understand this kind
  of source too.
- **AI-generated actions now really deliver the fields into the target.** Previously a draft might read the
  title / author but never put them into the SiYuan columns (or the Orca tags) — extracted fields and delivery
  parameters are two separate channels. Generation now fills in the column / tag plan from the variables it
  just extracted and names the columns it added; variables that ended up unused are called out as well, so
  nothing is fetched for nothing. Also: "None of these, let me point" now really takes effect (it used to be a
  false success — you clicked and nothing changed, neither on the page nor in the draft).
- **Importing someone else's action pack: you can see the problems before installing.** When you paste an
  action pack's JSON and hit "Parse preview", it points out the parameters that are wrong (which action, which
  parameter name it does not recognize, or which value has the wrong type) and says what that means: the
  action will run with defaults and do nothing useful. These used to surface only after installing and
  actually running that step. The preview is a heads-up only — it does not block you from installing.

## v0.29.0

- **AI-generated actions can actually read the values now.** The model used to guess selectors, so drafts often
  "looked right in the preview but came back empty when run". It now reads this page's structure first
  (which elements exist and what they say), and only writes a source into the config after it has been verified
  one by one. The result shows "how it found this" plus the real value on this page; when several candidates
  exist you can switch between them; fields it truly cannot read are left as a "Pick" button — click one element
  on the page and it is filled in.
- **The AI page is easier to use.** It shows candidates as soon as it opens, and no longer spends your model
  credits automatically (ask for more with "Think of a few more with the model" — the cost is written on the
  button). "Generate more precisely" is on by default and remembers your choice; generation shows progress in
  three stages; switching tabs and coming back no longer loses your intent, the generated draft, or the model
  connection you picked.
- **Generated actions no longer ship with references to variables that do not exist** (which used to produce
  dead actions) — those are stripped during generation. Card *content* (actors, cover image …) is now visible
  to the model, so share cards can be filled in.
- **One field can read differently per site**: the same field can use a different source on each site, and every
  source can be limited to "only on these pages". The trial run tells you outright "which source this site is
  using" or "why everything came back empty". AI now runs only for fields you have not read yet — faster and
  cheaper.
- **Article rules can be overridden and re-scoped**: a built-in rule can be taken over by your own
  (delete the override and the built-in one returns); which pages a rule applies to can be edited by hand and
  evaluated on the spot; the Studio lists every built-in rule.
- **Clipping reads the article more accurately**: built-in article rules for Xiaohongshu, X threads and others;
  the article template is configurable, and fields referenced in the template are now part of the dependency
  calculation (the X thread rule previously had no effect).
- **Stage a selection, then save a batch**: the selection capsule has "Add to staging"; save the whole batch to
  Orca Note / SiYuan in one go. The orb shows a staging count and the staging area sits at the top of the action
  list; when a page bubble covers the capsule, the right-click menu and the command palette can collect too;
  after saving, items are marked "saved" instead of being cleared.
- **New "Data" page**: import / export / backup / restore in one place; the whole config can be backed up and
  restored (secrets are never included), and article rule packs can be exported to share with others.
- **Scene trees support moving / copying across containers**: actions and groups can be moved between scenes.
- Fixes worth naming: the selection capsule now caps at 6 actions with a "⋯" expander; Xiaohongshu image walls
  no longer come out in the wrong order; array fields returned by a model are no longer crammed into one blob
  of JSON.

## v0.28.1

- Translation: the language-pack download notice now follows the real download event, instead of treating a
  finished (100%) download as a first-time download.

## v0.28.0

- Translation no longer needs any configuration: on desktop Chrome / Edge 138+ it now runs on the browser's own
  on-device translation — no API key, no cost, and the translation is produced on your computer without going
  through any server (including us); it works offline once downloaded. The browser fetches the language pack
  itself the first time you use a given language pair;
- Translation gained "save a translated page to your notes": a whole foreign article is translated into Chinese,
  shown in a bubble first, and only written to Orca / SiYuan when you click. Where the browser can't do it,
  it says plainly why;
- Polish, summary and AI summary are unchanged and still need your own AI connection.

## v0.27.0

- The UI now supports English: switch under Settings → Language (follow system / 简体中文 / English);
- New "See what you can do on this page": ask AI from the Studio's "AI" page (or the "✨ What can I do here"
  entry at the bottom of the orb panel) to look at the current page and suggest 3–5 candidate actions for this
  kind of page; click one to fill in the intent — it still goes through preview and only applies when you
  confirm; shuffle if they miss;
- The command palette can now use a sentence too: press Ctrl/⌘ + Shift + K and what you type appears under
  "Use this text…" to run actions that reference it — a shipped "Save a note" action stores one sentence
  straight into Orca Note / SiYuan;
- New "work on the text in the input box": put the caret in any site's input box, press Ctrl/⌘ + Shift + K
  (the palette lists these under "Use what's in the input box…") or right-click inside the box, and act on what
  you are typing — three ship out of the box: "Polish into Chinese", "Translate into Chinese" and
  "Translate into English". The result replaces the text in that very box, the caret parks at the end and focus
  stays in the box, and a bad pass is undone with Ctrl/⌘ + Z; if the page swapped that box mid-way, you typed
  more while waiting, the box is still mid–IME composition, or it is read-only, it aborts with an explanation
  and never overwrites what you typed ("Translate into Chinese / English" need no configuration at all — they
  use the browser's on-device translation, so the text never leaves your computer and costs nothing; only
  "Polish into Chinese" still needs an AI connection picked on the Studio's "Extract" page);
- The page right-click menu no longer stops at 8 items: extra entries used to be dropped silently, now it lists
  every action you ticked; it also shows up inside input boxes (our items are appended to the browser's native
  menu, so copy / paste keep working);
- Typing in our panels no longer fires the page's own shortcuts: keys like "c", "/" or "j" pressed in the
  command palette / in-page Studio / in a result dialog used to be picked up by GitHub, Gmail and others
  first — now they are not;
- The command palette now lists candidate actions across modes, greys out the unavailable ones and says why
  (e.g. "… needs a selection on the page first");
- The Studio's action detail area is reorganised: content scope / line breaks / auto-run / follow-up steps
  collapse into a one-line clickable header, and options irrelevant to the action collapse into a short note
  instead of dead knobs.

## v0.26.0

- The AI config assistant can now set up a whole set: describe what you want in one sentence and it drafts a
  single action, a batch of actions (with follow-up steps), or an entire mode — e.g. "build an Orca Note mode
  with bookmark, excerpt and task actions";
- It uses each capability's shipped recipes (save as bookmark / excerpt / task / full-page clip …) as the
  parameter baseline, so you get "recipe + your intent" instead of an empty shell;
- "Where it lands" is now confirmed in the preview: it suggests a new mode's "General" scene or a new scene in
  the current mode based on your intent, spells out each one's consequence (runs on any page / appears only on
  this site), and you can change it any time;
- New "auto-run": if you want an action to fire on matching pages, tick it explicitly in the preview — off by
  default, and the consequence is stated when you tick it.

## v0.25.0

- The About page now has "Contact" — my WeChat ID (click it to see the QR code) and email, both on one line;
- Fixed: zooming a QR code in the standalone settings page could push the overlay off-screen; it now stays
  centred inside the window (and shrinks first on short windows);
- More layout and wording cleanup on the About page: fewer rows and dividers.

## v0.24.0

- The About page has been reorganised — a tighter layout, a clearer hierarchy, and a new way to take part;
- The "Shortcuts" section on the Settings page now lists built-in actions correctly;
- Various stability and internal improvements.

## v0.23.0

- Command palette: press Ctrl/⌘ + Shift + K on a page — type a few letters to filter and press Enter to run one
  of this page's available actions; the palette also has commands like Open settings / Page variables /
  Extraction / Activity / Preferences;
- Changeable shortcut (extension): uses the browser's native shortcut page (chrome://extensions/shortcuts, or
  edge://extensions/shortcuts on Edge); a new "Shortcuts" section on the Settings page shows the current
  binding (and warns when it's unbound); the userscript's keys are fixed and can't be changed;
- Right-click menu (extension): right-click a page → the "Shunshou" submenu lists this page's available actions,
  plus "Open toolbox / Page variables";
- Finer per-site control: four entry points (orb / command palette / right-click menu / selection capsule);
  "Dock only" keeps the orb + command palette + right-click menu, with a per-surface advanced escape hatch;
- The result dialog gains "Run details": every step and the reason for any failure (a failed step offers a
  one-click "Go to config"); when the deliveries are copy / download only and all succeed, the dialog closes
  itself (click to cancel);
- Actions panel: the ✎ to the right of an action jumps to its config, and "Page variables" now sits at the
  bottom in the "Page info" area.

## v0.22.0

- "AI config assistant": on the Studio's "AI" page, describe what you want in one sentence (e.g. "clip this kind
  of page's article ad-free" or "extract the author and rating into SiYuan") and AI drafts a config —
  capability, params, action chain, content scope, and variables included; nothing changes until you confirm,
  then click "Apply" (one-step undo);
- Action chains ("follow-up steps"): after the main action succeeds, the next ones run in order (e.g. save to
  Orca Note, then write a SiYuan row); a step can be set to "wait for my confirmation";
- Config generation uses the current page's structure: selectors are verified on the page and ones that match
  nothing are dropped;
- Several real-device fixes make AI generation more reliable.
