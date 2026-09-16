<!--
  English translation of README.md (甲档第二步 / English docs step 2).
  Structure, links and screenshots mirror the Chinese version one-to-one.

  Reviewer decisions (2026-09-18; updated 2026-10-01):
  - Patron list is NOT duplicated here: `pnpm gen:patrons` only writes README.md's marker block,
    so this file links to the Chinese README instead (avoids staleness).
  - The UI ships with a language switch (Settings → Language: follow system / 简体中文 / English);
    quoted UI labels below are the English UI strings.
  - Author pen name 养恐龙 is kept in Chinese (brand.ts has no English form).
  - Path examples use `Shunshou/...` (brand folder) as an illustration.
-->

<p align="center">
  <img src="assets/icon-128.png" width="96" alt="Shunshou">
</p>

<h1 align="center">Shunshou · Context-Aware Web Toolbox</h1>

<p align="center"><a href="./README.md">中文</a> · English</p>

<p align="center">Whatever you're doing on the web, done right at hand.</p>

<p align="center">
  <a href="https://github.com/hqweay/shunshou/releases/latest"><img src="https://img.shields.io/github/v/release/hqweay/shunshou?label=Latest" alt="Latest version"></a>
  <a href="https://github.com/hqweay/shunshou/releases"><img src="https://img.shields.io/badge/Platform-Chrome%20%2F%20Edge%20%2F%20Userscript-4285F4" alt="Platform"></a>
  <a href="https://shunshou.leay.net/"><img src="https://img.shields.io/badge/Website-shunshou.leay.net-0969da" alt="Website"></a>
</p>

<p align="center">
  <img src="assets/screenshot-dock.png" alt="The floating orb matching actions to the current page automatically">
</p>

Shunshou is a browser extension (Chrome / Edge) — and also a **userscript** that installs on desktop and mobile: it notices which page you have open and quietly swaps in the right actions — save books, movies, and games from Douban, collect videos, comments, and subtitles from Bilibili, turn X / Xiaohongshu / Instagram posts into cards in one click, send your selection to Orca Note / SiYuan. When you want to share something, a quote or a long article, a whole page of text and images is ready in a moment. Things you do often can even be set to "auto-run" — open the matching page and they run for you (unless the site is set to "Quiet" or "Off").

- **No account, no server**: config and secrets stay on your machine; content is only sent to the notes / model services you configure yourself
- **Context-aware**: built-in scenes for GitHub, Douban, Bilibili, X, Xiaohongshu, Instagram and more; every other page gets generic actions like bookmark, excerpt, full-page clip, and share
- **Edit inside the box you were typing in**: put the caret in any site's input box, press `Cmd/Ctrl+Shift+K` (same key in the userscript; the right-click menu is extension-only), and act on **the text you just wrote** — "Polish the text in the input", "Translate the text in the input" and "Translate the text in the input into English" ship out of the box (pick an AI connection on the Extract page first). The result is **written back into that box** instead of copied somewhere else, and a bad result is undone with `Cmd/Ctrl+Z`. While the model works, the palette leaves a "Running…" line in place, so you never think your click missed
- **Can step in, can step back**: per-site control — a site can be set to "Dock only" (the orb, the command palette and the right-click menu stay; only the selection capsule is hidden) or "Selection only", to "Quiet" (no auto-run, no suggestions), or fully "Off" (no UI mounted, and it isn't counted in your browsing footprint either); one click on "This site" at the top of the orb panel toggles it, and you can resume anytime
- **Clean clips**: built-in site rules (Douban books/movies, GitHub, Bilibili, WeChat Official Accounts, SSPAI) are accurate out of the box, and other pages use the article engine to detect the main content automatically. If it's off, use "pick content" — click containers (you can select several), and it takes effect immediately; you can also save it as a site rule
- **Built to keep**: clips, share cards, and articles can all be **saved as local files** (Markdown / text / images); paths support variables and subfolders, e.g. `Shunshou/{{date:YYYY-MM-DD}}/{{title}}.md`, ready to drop straight into your Obsidian / SiYuan vault; with Obsidian installed you can also **save straight into your vault in one click** (an `obsidian://` deep link, with a configurable folder inside the vault)
- **Selection-first**: select some text and quick actions like "Excerpt / Post to X / Save to notes" appear right above the selection — **"Translate" is among them and works out of the box**; the translation shows in a floating bubble beside the selection (draggable, copyable; decide whether to share after reading). By default it runs on the browser's built-in on-device translation: **no cost, and the text never leaves your machine**
- **Chainable**: actions can carry "then do" steps — one click runs the whole chain (save to Orca, then write to SiYuan; save, then copy the link…); steps can also be set to "wait for my confirmation", so they don't run automatically and wait for you on the result surface
- **Hands-on**: actions can be set to "auto-run" or "suggest only" — run for you when the matching page opens (as long as the site isn't set to "Quiet" or "Off"), or just give you a nudge (off by default, enabled per action, with delay, cooldown, and ask-before-running options); chains can also click buttons, fill inputs, wait for elements, and capture page elements as images
- **No code required**: actions, matching rules, extraction fields, and content templates are all adjusted visually in the Studio, and mistakes can be undone in one click
- **Extensible**: optionally connect your own AI model (or describe what you want and let AI set the action up for you, or ask it what you could do on this page); you can also install actions others have made from the "Action Market"

*The interface follows your system language and can also be switched explicitly under Settings → Language (follow system / 简体中文 / English).*

## Installation

**Browser extension (recommended on desktop):**

**Chrome Web Store (recommended)**: [Shunshou · Context-Aware Web Toolbox](https://chromewebstore.google.com/detail/adnmpjgdmlhncmdfmfniippjefekdhfl) installs in one click and updates automatically.

**Edge Add-ons**: [Shunshou · Context-Aware Web Toolbox](https://microsoftedge.microsoft.com/addons/detail/elhiacffkdkpkcegafabljaldcoimich) also installs in one click and updates automatically.

**Or load it manually** (it also works in other Chromium browsers):

1. Download the latest `shunshou-extension-*.zip` from [Releases](https://github.com/hqweay/shunshou/releases/latest)
2. Unzip it to any folder (don't double-click it to run directly)
3. Open `chrome://extensions` → turn on "Developer mode" in the top right → "Load unpacked" → select the unzipped folder

> **Live on both the Chrome Web Store and Edge Add-ons** — one-click install with automatic updates either way; the manually loaded build from Releases works just the same.

**Userscript (for phones, or when you'd rather not install an extension):**

Install a userscript manager first, then open the install link (the manager checks for updates automatically):

- **Desktop**: install [Tampermonkey](https://www.tampermonkey.net/) or [Violentmonkey](https://violentmonkey.github.io/) in Chrome / Edge / Firefox
- **Android**: install Tampermonkey / Violentmonkey in [Firefox for Android](https://www.mozilla.org/firefox/browsers/mobile/android/) (or another extension-capable browser such as Kiwi)
- **iOS / iPadOS**: install [Userscripts](https://github.com/quoid/userscripts) (free on the App Store) or Tampermonkey in Safari

Install link (or create a new script in the manager and paste the contents):

**https://github.com/hqweay/shunshou/releases/latest/download/shunshou.user.js**

> **On mobile**: the injected UI is adapted to narrow screens and touch — the floating orb sits in the bottom-right; tap it to open the actions panel. Actions pinned beside the orb are always visible on touch devices (phones have no hover), and "In-page config" fills the screen.
> A few desktop-only capabilities **degrade explicitly** and say so (browsing footprint covers only the current tab, saved-file subfolders are flattened, cross-tab stats are unavailable); the features themselves are still there.

> **The first install opens a one-time "Get started" page** (a three-step checklist in the Studio: meet the UI → set up a connection → run your first action); once you run your first action it retires itself, and "About" keeps a "See the intro again" link.

## Three-minute setup

1. **Open any page**: a floating orb appears in the bottom-right (except on sites you set to "Off"); on GitHub / Douban / Bilibili / X / Xiaohongshu and other pages it switches to the matching scene automatically
2. **Select some text**: a small capsule floats above the selection — click "Share excerpt / Post to X / Save excerpt"; you can also use actions from the orb.
   Select a sentence in a foreign language and click "**Translate**" — the translation appears right next to the selection (without leaving the page; the bubble is draggable)
3. **Open a good article**: click "Share full text" to lay the whole article and its images out as a card (very long ones paginate automatically, nothing gets cut off);
   click "Copy page clip" to copy it as Markdown (with image links) that pastes straight into Obsidian / Notion / SiYuan; to save it as a file directly, click "**Save Markdown locally**" — it lands in `Downloads/Shunshou/date/title.md`; with Obsidian installed, click "**Save to Obsidian**" to write it straight into your vault
4. **Configure**: the gear "**In-page config**" at the top of the orb panel opens right in the page — try fields / clips against the current page and pick article containers; the **✎** to the right of any action jumps straight to its config;
   clicking the extension icon in the browser toolbar → "Open Studio" gives you a standalone tab

## Features

### Entry points: how to open it

There are several entry points — use whichever you like:

- **The orb** (default): bottom-right of the page; tap it to open this page's actions panel. Drag it to snap it to the edge, hover to expand, or pin your frequent actions beside it
- **Command palette**: press `Ctrl/Cmd + Shift + K` on a page — type a few letters to filter, then press Enter to run one of this page's available actions. **What you type can also be used as input** — the palette's "**Use this text…**" section lists actions that reference `{{input}}` (a shipped "**Save a note**" action stores one sentence straight into Orca Note / SiYuan); press Enter to run. The palette also has a "Commands" section (Open settings / Page variables / Extraction / Activity / Preferences). In the **extension you can change this shortcut in the browser** (`chrome://extensions/shortcuts`, or `edge://extensions/shortcuts` on Edge); the "Shortcuts" section on the Settings page shows the current binding and warns you when it's unbound. The **userscript's keys are fixed and can't be changed** (if they're taken, open the command palette from your script manager's menu)
- **Right-click menu** (extension only): right-click a page → the "Shunshou" submenu lists this page's available actions, followed by "Open toolbox / Page variables". The menu is built from the actions the page has **already worked out**, cached per tab in local memory — it does **not additionally read page content, nor the tab's address** It shows up **inside input boxes too** (e.g. right-click a sentence selected in a comment box to polish or translate it) — our items are **appended to** the browser's native menu rather than replacing it, so copy / paste still work. The menu lists **every** action ticked for "right-click menu" with no count-based truncation — narrow it by unticking that chip per action in the Studio
- **Selection capsule**: appears above your selection when you select text (see "Selection-first" below)

### Context-aware: site scenes

| Site | What Shunshou can do |
|---|---|
| GitHub | Copy `owner/repo`, generate a repository share card |
| X (Twitter) | Tweet text + images: copy the text, generate a share card, prefill a new post; an **author's thread (the whole series)** can also become a card or a note (via the "X thread → notes" pack in the Market) |
| Xiaohongshu | Note title / text / **all images** (carousel auto-completed) and like-save counts: copy the text, generate a share card |
| Instagram | Post images auto-completed into an "image wall": copy the text, generate a share card (with author / date / likes) |
| Douban (books / movies / games) | 17 / 20 / 11 fields extracted automatically (movies and TV share the same set: format / episode count / synopsis, etc.): copy the info, share card, write to Orca / SiYuan |
| Bilibili videos | Video info + comments (including replies) + **subtitles** (CC / AI-generated, requires a Bilibili login): copy, generate a share card, save as a video note, save subtitles to your notes or let **AI summarize the subtitles** (summary + key points) |
| Any page | Copy Markdown link / excerpt, save as bookmark or task, full-page clip, **save Markdown locally**, **save to Obsidian**, AI summary, **selection translation**, **save a translated page to your notes** (on-device translation → Orca / SiYuan), share card, post to X; click / fill / wait / **write back to the input box**, element screenshots (multiple blocks / stitched long image) |

The orb can be dragged to snap to the edge, hovered to expand persistent actions, and used to switch scenes manually at the top of the panel. It can also switch **modes** — modes are organized by purpose (out of the box: Daily / Work / Study / Marketing — Daily needs zero setup, Work and Study write to notes, Marketing makes cards and posts), and a mode is a whole set of scenes, so switching one mode swaps your entire workflow instead of editing actions one by one. Backends such as Orca / SiYuan / AI models are global **connections**: configure one and its actions show up automatically. Actions can be grouped (there are "Share" and "AI" groups out of the box), and collapsed state is remembered.
Actions that aren't set up yet (say, no notes connection chosen) are tucked into the "Unconfigured" section at the bottom of the panel and appear automatically once configured.

### Clean clips: content scope and site rules

- **Accurate by default**: built-in site rules cover Douban books/movies, GitHub, Bilibili, WeChat Official Accounts, and SSPAI; other pages use the article engine (Readability)
  to detect the main content automatically. Hidden content (including ads hidden by ad blockers) doesn't make it into the clip
- **Pick when it's off**: In-page config → "Site rules" → "Pick content" → click containers on the page (**multi-select supported**, press Enter to finish; a single paragraph or short quote counts)
  → choose the scope (whole site / this kind of page) → save and it takes effect; "Diagnose this page" tells you the source, which rule matched, and how many characters each block clipped;
  deleting a rule falls back to the system default, and built-in rules can be disabled individually too
- **One scope per action**: the action's expanded panel has "**Content scope**" to set it just for that action — pick containers (multiple blocks merge),
  "pick at run time", or reference a site rule as a base and override only the parts you want (including remove / keep cleanup and the image threshold).
  That's why "Save article" and "Save comments" don't step on each other
- **Article line breaks** (per action, in the expanded panel): treat single line breaks as paragraphs / 1 or 2 line breaks between paragraphs (SiYuan semantics: 1 = line break in the same block, 2 = new block) /
  collapse consecutive blank lines — only affects article-type variables, Markdown clip structure is untouched; the old global setting on the Settings page is written into each action once after upgrading
- **This-run pick → long-term rule**: the containers / excluded blocks you pick with "**Set this run's content scope**" at the bottom of the orb apply to this run only;
  once you're happy, "**Save as rule**" promotes them into a site rule (whole site / this kind of page) that takes effect automatically next time
- **Save as variable**: the neighbouring "**Save as variable**" stores an element on the page as a named variable (written to config, reusable across runs),
  for use as `{{field.*}}` in content templates or AI prompts

### Selection-first

Select text on a page and a small capsule appears above the selection — it lists only the actions that **actually use the selection** (usually just two or three; the rest go into `⋯`):

<p align="center">
  <img src="assets/screenshot-selection.png" width="860" alt="Selection capsule">
</p>

- Clicking the capsule won't clear your selection; scrolling, clicking blank space, or pressing `Esc` dismisses it; if you don't like it you can turn it off on the Settings page and keep using the orb as usual
- **Selection translation (works out of the box)**: select a sentence → click "Translate" → a small bubble appears next to the selection **showing the translation in place** (without leaving the page or switching tabs);
  the bubble can be **dragged** out of the way of the text it covers, and copied in one click. When you're happy with the translation, the bottom of the bubble also offers "Share card / Post to X" —
  **decide after you've read it**; nothing is posted for you automatically. By default this runs on **your browser's built-in on-device translation** (desktop Chrome / Edge 138+): **no connection to configure, no cost, and the translation is generated on your computer without going through any server**
- To pin where an action shows up: each action row in the Studio has a persistent **"Panel · Capsule · Right-click · ★" visibility cluster** (show in the orb panel / show in the selection capsule / show in the right-click menu / pin next to the orb). The indicator shows **whether it will actually appear** — an action that references the selection will not show in the capsule, and one that does not reference the input box will not show in the "use what's in the input box…" section, so a lit chip really does appear
- **Open link / search selection**: splice the selection or a field into a URL template and open it directly (customizable — e.g. `mailto:`, `obsidian://` deep links);
  a built-in "Search Bilibili" example, with variables URL-encoded automatically

### Working on the text in an input box

Put the caret in any site's input box and press `Ctrl/⌘ + Shift + K` — the command palette grows a
**"Use the input box…" section** that lists only the actions that really use what you typed, and shows you
the exact lines it picked up:

<p align="center">
  <img src="assets/screenshot-palette.png" width="860" alt="The command palette's &quot;Use the input box…&quot; section">
</p>

- The result **replaces the text in that very box** (the selected part; the caret parks at the end and focus stays in the box), and a bad pass is undone with
  `Ctrl/⌘ + Z` — it goes through the browser's own edit stack, not "copy it elsewhere and paste it back"
- Three ship out of the box: **Translate into Chinese** and **Translate into English** (for writing Chinese on an English page) run on **the browser's built-in translation with zero configuration**; **Polish into Chinese** needs your own AI connection. The same shape lets you add your own: create an action, pick the "write into the input" capability, and reference `{{page.input}}` in the template (selection first, whole text when nothing is selected)
- Don't want to open the palette? **Right-click inside the input box** and the same group is in the "Shunshou" submenu (extension only; our items are
  appended to the browser's native menu, so copy / paste keep working)
- Four guards: the page swapped that box mid-way, you typed more while waiting, the box is still mid–IME composition, or it is read-only — **any of these aborts
  with an explanation and never overwrites what you typed**; on failure the result is attached to the message so you can copy it by hand
- It touches **only the one editable you have focused**, never scans the page, and **never reads password fields**

### Sharing

- **Share card**: select → a clean card; delivery is handled by "then do" steps — the image stays in the result dialog to copy / download on demand, and you can add
  "Save image file" in the action. Four themes (paper / ink / brand / pure white),
  four sizes (long / 4:5 / 3:4 / 1:1), content blocks can be added, removed, and reordered, and the bottom-right carries a QR code to the source page by default;
  the body supports **inline styles** (bold / italic / inline code / strikethrough / highlight / links)
- **Preview as a workbench**: after rendering, a preview opens — "Adjust" lets you switch theme / background color / font directly and edit the card content;
  "Share full text" also lets you edit this run's article in place (affects this run only, not saved to config), and "Save to action" when you're happy; if the image is too long to read, click it to "View full size"
- **Share full text / page clip**: the whole article and its images are laid out **in reading order** as a card, and very long ones split into several images with nothing cut off
  (copy them one by one / download all from the result dialog — no automatic clipboard grab; "Copy" just copies, it won't stuff files onto your disk);
  it can also be copied as Markdown in one click (with image links, ready to paste into Obsidian / Notion / SiYuan)
- **Save as local files**: full-page clips / share cards / text can all be saved as local files (Markdown / text / images),
  and paths support variables and subfolders — e.g. `Shunshou/{{date:YYYY-MM-DD}}/{{title}}.md`, ready to drop straight into your Obsidian / SiYuan vault;
  names are auto-numbered on collision, and once the extension has the "Manage downloads" permission you can also choose to overwrite. Files are only written to your own Downloads folder — your existing download history is never read or listed
- **Save to Obsidian**: with Obsidian installed, write a page clip straight into your vault in one click — via an `obsidian://` deep link handed to Obsidian, with no server in between;
  the path inside the vault supports subfolders (e.g. `Shunshou/{{date:YYYY-MM-DD}}/{{title}}`), collisions can append or overwrite, and by default the note doesn't pop open.
  Set a vault name once and you're set (leave it empty to use the current vault)
- **Share to social platforms**: X / Weibo / Bluesky / Telegram / Mastodon / Reddit — opens the platform's official share dialog with the content prefilled;
  no account or credentials needed, and you confirm in the editor before posting
- **Result dialog**: each delivery target reports its status, and failed ones can be retried; the "**Run details**" section lists every step and the reason for any failure
  (a failed step offers a one-click "**Go to config**"); when the deliveries are copy / download only and **all succeed**, the dialog closes itself after you copy or download
  (clicking it or moving the mouse in cancels the close, so it never disappears on you)

<p align="center">
  <img src="assets/screenshot-result.png" width="860" alt="Result dialog: preview + adjust">
</p>

<p align="center">
  <img src="assets/screenshot-card.png" width="400" alt="A card generated from Share full text">
</p>

### Save to notes (optional)

- **Orca Note**: MCP endpoint + Token + repository ID; tags and properties are created / filled in automatically per the scheme (types are coerced automatically)
  - Bookmark / excerpt / task: the content shape is just a template, change it however you like
  - **Full-page clip / web summary**: the page title is the parent block (filed under the "Bookmark" tag), and the article (or AI summary) becomes its child block;
    page info (links, etc.) is stored as properties per the "Bookmark" tag scheme; content hidden on the page (including ads hidden by ad blockers) doesn't make it into the clip
- **SiYuan**: kernel address (default `http://127.0.0.1:6806`) + API Token, three targets:
  - **Database (attribute view)**: write a row; the column scheme is edited visually and missing columns are created automatically; **duplicate check before saving** — when a row with the same name already exists,
    a dialog asks "Update / Skip / Create new" (Skip by default, protecting cells you edited by hand); **image columns are localized automatically** — Douban covers and the like are downloaded and
    stored in the SiYuan asset library, so thumbnails show up in the database instead of broken images (you can switch to "Keep original link")
  - **Document / daily note**: pick a notebook first; leaving "Target document" empty means **today's daily note** (located automatically, created if missing),
    or save to a specific document (created automatically if not found); content and insertion position (end / beginning) are configurable
  - **Document database**: create the content as a new SiYuan document and **bind** it into the chosen database — it can follow the database's "item template",
    or use a custom save path (e.g. `/Collection/{{dateText}}/{{title}}`); article images are uploaded to the SiYuan asset library by default.
    **Works out of the box**, plus an **AI summary** variant (first use AI to summarize the whole article into structured Chinese, then save it; requires an AI connection)
  - **Save a translated page to your notes**: a whole foreign article is translated into Chinese with **your browser's built-in on-device translation** (desktop Chrome / Edge 138+, zero configuration, no cost, **the text never leaves your machine**); the translation is **shown in a bubble first**, and only when you click "Save to Orca / Save to SiYuan" is it actually written. Where the browser can't do it (userscript host, older browsers, phones) it says plainly why
- **Image lists in templates**: when you insert a "one URL per line" image list (`{{field.*.images}}` / `{{page.images}}`) into the body, add the `:md` hint
  (e.g. `{{field.<group>.<key>.images:md}}`) to render it as Markdown images and localize them along with the body — no hand-written `![](...)` needed
- **Clip fidelity**: article clips keep links, emphasis, **formulas** (common forms such as KaTeX / MathML, written as `$…$` / `$$…$$`), and nesting;
  when the target is **SiYuan** it switches to the SiYuan kernel converter for higher fidelity (headings, merged table cells, and code blocks all come through)

### Then do (action chains)

An action can carry a series of **follow-up steps**: after the main step succeeds they run in order, and any failure stops the chain; page info is extracted once and shared by the whole chain.

- Example: **Save to both libraries** — save an Orca bookmark, then write a row to a SiYuan database (one click, both libraries populated)
- Example: **Save and share** — save a bookmark, then copy "《Title》 Link" to the clipboard
- **"Wait for my confirmation" = a "Next step" on the result surface**: some steps shouldn't run automatically — an AI translation, for instance, you want to glance at before deciding whether to save it to
  Anki / share. Mark a step "wait for my confirmation" and it won't run with the chain; instead it shows up on the **result surface** (the selection-translation bubble, the result dialog) and runs only when you click it.
  The built-in "Translate" ships with two: share card (original + translation) / post to X (translation + link)
- Add steps by expanding an action on the Studio's "Scenes" page; the two examples above are ready-made action packs: Studio → "**Market**" → fetch → install

### Automation (auto-run · page actions)

Every action has a "trigger" — manual / **auto-run** / **suggest only**:

- **Auto-run**: runs for you when a matching page opens, no click needed (as long as the site isn't set to "Quiet" or "Off"). It's **off** by default, enabled per action, and you can set a
  **delay** (wait for rendering / lazy loading), a **cooldown** (minimum interval), a dedupe scope (every visit / once per document), and
  **ask before running** (recommended for side-effecting actions like writing to notes). Nothing is set to auto-run out of the box;
  action packs from the "Action Market" that ship with auto-run are **off after installation too** — whether to turn it on is always your call
- **Suggest only**: doesn't run, just shows a small dot on the orb to remind you "there's something you could do here"
- **Quiet sites**: set a site to the "Quiet" tier and its UI stays, but it never triggers automatically (you can still open the orb manually). Studio →
  "**Run → Automation**" lists all enabled auto-runs in one place, lets you tune parameters in place, and shows recent runs; the quiet list now lives under "**Run → Sites**" (see below)

**A few things you can do**:

- **See it, log it**: auto-run "Save as movie / book / game (SiYuan)" on Douban book / movie / game pages — browse and it's in your library,
  with no clicks at all; turn on "ask before running" if you'd rather confirm before writing
- **Expand, then clip**: chain "**Click** 'Expand full text' → **Wait** for the element → **Copy page clip**" in one action —
  works for collapsed comments and lazily loaded long articles
- **Select and search**: pick the site's search box and have "**Fill input**" use `{{selection}}` — select a phrase and click once to fill it in
- **Polish while you type**: type an English sentence in a comment box or search box, press `Cmd/Ctrl+Shift+K` → "Translate the text in the input" → the result **replaces the text in that very box**, caret parked at the end of the translation, and you keep typing; `Cmd/Ctrl+Z` takes you back to your own sentence. No window switching, no copying elsewhere
- **Chinese into English**: the same path in reverse when you are writing Chinese on an English page (a reply, a comment, a support ticket) — "Translate the text in the input into English", whose prompt asks for what a native speaker would actually say rather than a word-for-word rendering
  (React-controlled search boxes work too)
- **Auto-archive**: open a report / dashboard page and automatically **capture a chosen area as PNG** and save it; you can also capture after a "click open"
- **Stitch a long image**: pick **several blocks** at once to screenshot them one by one, or **stitch them vertically into one long image** — a whole timeline's posts, several tables on a page, anything can go together
- **Notify me after it saves**: add a "Send notification" step at the end of the chain (Studio "New from capability"), so it tells you the result once it's done

**The page-action quartet** (click / fill / wait / **write back to the input box**, building blocks in a chain): for the first three you don't write selectors by hand — use "**Pick**" next to the parameter and click on the page. **Write back** needs no selector at all: it targets *the box you are typing in right now* (reference `{{page.input}}` in a template to get that text), replaces the selected part, leaves the caret at the end, and hands focus back to the box.
All four are **synthetic events and best-effort**: rich text editors (Slate / ProseMirror types) and file uploads are not promised, and sites with bot protection may not respond.

Write-back also has four guards: the page replaced that input box while the model was thinking, you typed more while waiting, the box is still mid–IME composition, or it is read-only. **Any of these aborts with a plain-language message and never overwrites what you typed**; on failure the result is attached to the message so you can copy it by hand.

**Element screenshots**: capture any element on the page (table / chart / card) as PNG, then copy or save it; the selector is picked the same way —
**multi-select several blocks at once** to export them one by one, or **stitch them vertically into one long image**.

### Per-site control

Don't want a site to get in your way — a dashboard, your bank, an intranet page — just add it to the list.
One rule = a set of URL patterns + one tier. There are **four entry points** to control: the orb, the command palette, the right-click menu (extension), and the selection capsule. Pick from five tiers:

- **Normal**: the default — all four entry points are available on every site (nothing to configure)
- **Quiet**: the entry points stay, but actions never auto-run and no suggestion dots appear
- **Dock only**: keeps every manual entry point — the orb **plus the command palette and the right-click menu** — and hides only the selection capsule
- **Selection only**: keeps only the selection capsule and hides the other three
- **Off**: nothing runs at all — no entry point is mounted, and the visit isn't counted in your browsing footprint either (a refresh makes it fully take effect)

**How to use it**: on the page you want to handle, click "**This site**" at the top of the orb panel — one click
toggles between "turn this site off" and "resume it"; press and hold (or click the "**⋯**" next to it) to pick one of
the five tiers and the scope (this site incl. subdomains / this page only), with "**All sites…**" at the bottom opening the list.
**How to get back**: once a site is set to "Off" there's no entry point left on the page — click the extension
icon in the browser toolbar (on the userscript, use "Resume this site" in your script manager's menu) and choose
"Resume here" in the current-site block (the page reloads automatically); you can also manage it under Studio
"**Run → Sites**", or hit "**Undo**" on the notice that appears.

The list lives in Studio under "**Run → Sites**": switch tiers, tick individual surfaces, reorder with ↑↓
(**a lower rule overrides one above it**), and delete. No new permissions, and the default is unchanged —
every site stays available; exclusions are ones you add on purpose.

### AI config assistant (plain-language setup)

Not sure how to configure an action? On the Studio's **"AI"** page, describe what you want in one sentence (e.g. "clip this kind of page's article ad-free", "extract the author and rating into SiYuan", or "build an Orca Note mode with bookmark, excerpt and task actions"), and AI drafts a **config** — **a single action, a batch of actions (with follow-up steps), or a whole mode**:

- **Don't know what to do here? Just ask**: the AI page's "**See what you can do on this page**" button (there's also a "✨ What can I do here" entry at the bottom of the orb panel) sends the **current page's text and structure summary** to the model when you click it, and returns 3–5 candidate actions for **this kind of page** — click one to fill in the intent, then it goes through the same generate / preview / apply flow below, **without touching your config behind your back**; click "Shuffle" if they miss. Suggestions are page-type level (and account for the connections you've configured), not just about this one article
- **Built on shipped recipes**: the recipes a capability ships with (save as bookmark / excerpt / task / full-page clip …) act as the parameter baseline, so you get "recipe + your intent" instead of an empty shell
- **Nothing changes until you confirm** (zero side effects); the preview is a plain-language summary plus read-only cards — click "Apply" when happy, and **undo in one step**
- **Landing and auto-run are confirmed in the preview**: it suggests a new mode's "General" scene or a new scene in the current mode from your intent, spells out each one's consequence (runs on any page / appears only on this site) and lets you change it any time; auto-run is opt-in there too, with its consequence stated — **off by default, unticked means it never runs**
- It reuses the OpenAI-compatible connection you set up on the "Connections" page; when generated from the **in-page** Studio it also gets a **structure summary of the current page** (class / id vocabulary), and the selectors it writes are verified **on this page** (ones that match nothing are dropped or flagged)
- In-page fallback: the standalone options page can't read page structure, so it only generates from your text intent (variable groups / ad removal unavailable, and the panel says so)

<p align="center">
  <img src="assets/screenshot-ai.png" width="860" alt="AI config assistant: one sentence generates a mode plus a batch of actions, with the landing spot confirmed in the preview">
</p>

### AI extraction (optional)

Connect your own OpenAI-compatible model (DeepSeek / OpenRouter / SiliconFlow / local Ollama all work):

- **The prompt is the config**: hand `{{content}}` (selection first, whole page if nothing is selected), `{{page.clip}}` (full-page clip) to the model,
  and it produces **custom fields** like summary / tweet copy / keywords; the fields are used in any action template just like ordinary variables
- Ready-to-use actions out of the box: "Summarize and post to X" (selection → AI summary → open X prefilled), "Copy AI summary", "AI summary card",
  **"Selection translation"** (selection → show the translation in an inline bubble, then share card / post to X), and "Save as web summary (Orca)" which saves a full-page AI summary to Orca;
  with only one AI connection it's bound automatically
- There's a progress indicator before the call, and results are cached for the session (no double billing); actions without a connection are collected in the "Unconfigured" section; content is only ever sent to **the endpoint you configured yourself**

### Action Market

- Subscribe to the official catalog on the Studio's "Market" page: **fetch → browse by tag / search → install**; utility actions are merged into the "always visible" layer automatically,
  and sites are packaged as new scenes; dependencies and conflicts are reported
- Installed packs can be "Check for updates" and "Uninstall" (variable groups / prompts that came with the pack are only cleaned up when nothing references them)
- Action packs are **pure data** (actions / extraction rules / prompts) with no code or secrets; you can also export scenes you've configured as a
  `.action-pack.json` to share with friends

### Studio and extraction

The Studio has nine pages — "Scenes / AI / Market / Extract / Connections / Run / Settings / Thanks / About"; all changes take effect immediately, with **Ctrl/⌘+Z to undo and Ctrl/⌘+Shift+Z to redo** (50 steps per session).

The "Extract" page turns "web page → variables" into visual configuration: a field source can be a selector / "label:value" / meta / JSON-LD / URL regex / selection /
template / try in order (fallback chain), and you can add transform chains (trim / replace / regex extract / truncate / split / default value);
there are 5 **system variable groups** out of the box (GitHub, web Meta, Douban books/movies/games) — click "Override" to change them; by default an override applies only to the current site and other sites fall back to the system version automatically.
There are also built-in placeholders like `{{page.text}}` / `{{page.clip}}` / `{{page.table}}` / `{{selection.context}}` / `{{clipboard}}` / `{{pick.*}}`, read lazily by reference — untouched if unused.
"Try" shows each field's value instantly:

<p align="center">
  <img src="assets/screenshot-extract.png" width="860" alt="Extract page: system variable groups and Try">
</p>

<p align="center">
  <img src="assets/screenshot-studio.png" width="860" alt="Studio: scenes and action tree">
</p>

- If you write JS, you can write local scripts under "My scripts" (input `{ url, title, selection, document }`, may return a Promise) —
  stored only on your machine, **not in the config and not included in export / sharing**; on first use in the extension, turn on "Allow User Scripts" on the extension's details page
- The "Run" page has five tabs: **Action usage** (last-7-days trend, 12-week heatmap, most-used actions, which actions you've never used),
  **Browsing footprint** (local dwell time / site ranking; on by default, can be turned off or cleared at any time),
  **Automation** (the list of actions with auto-trigger enabled + tune "suggest only / delay / cooldown / ask before running" in place, plus recent auto-runs;
  "Quiet" sites skip all auto triggers first),
  **Sites** (the per-site control list: Normal / Quiet / Dock only / Selection only / Off, with per-surface advanced options and ↑↓ reordering),
  **Issues** (config health check + recent run errors)
- The "About" page lets you manually **check for updates** (it only requests public version info from GitHub when you click)

## Updating

**Extension**: download the latest zip and go through "Load unpacked" again (your config is kept).
**Userscript**: your userscript manager checks for updates automatically; usually nothing to do.

You can also click "**Check for updates**" on the Studio's "**About**" page to see if there's a new version; new default scenes / actions in a new version are delivered
incrementally the next time you open it — what you changed stays, and what you deleted doesn't come back.

## Privacy

Shunshou doesn't collect or upload any data; there's no account and no server. Config and secrets stay on your machine,
and writing to notes / calling models talks directly to the services you configure. "Save locally" only writes the current file to your own Downloads folder and never reads your existing download history. See the [Privacy Policy](PRIVACY.en.md) for details.

## Thanks

Shunshou is free, ad-free, and account-free. Thanks to everyone who has put their stamp on it — the extension's "Thanks" page shows the same wall of stamps. The live list lives in the [Chinese README](./README.md).

## Feedback

- [Issues](https://github.com/hqweay/shunshou/issues): problems, suggestions, or a new site you'd like
- Author: 养恐龙 · [Blog](https://leay.net/)

---

<p align="center"><sub>Shunshou · Context-Aware Web Toolbox · Local-first</sub></p>
