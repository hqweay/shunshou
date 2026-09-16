# Privacy Policy

[中文](./PRIVACY.md) · English

> The privacy policy for "Shunshou · Context-Aware Web Toolbox" (browser extension / userscript).
> Last updated: 2026-09-17

## In one line

Shunshou does not collect, store, or upload any of your data. There is no account and no server.

## How data flows

- Page content is read and rendered locally in your browser only when **you trigger an action** (by clicking, or when you have enabled "auto-run" for that action); auto-run is off by default, enabled per action, and runs only on matching pages that are currently open.
- Writing to notes: content is sent directly to the note service you configure (Orca Note MCP endpoint / SiYuan kernel address), with no third-party relay.
- Saving to Obsidian: content is handed to the **Obsidian app installed on your machine** via an `obsidian://` deep link (the body goes through the system clipboard); it is not sent to any network service and does not pass through us.
- Generating a share card: the image is drawn locally in the browser with Canvas; cover images and the like are fetched from the target page / image host.
- Using **AI extraction** (only after you enable and configure it): page content / your selection is sent to the **model endpoint you choose** (if you configure a local model, it never leaves your machine); it does not pass through us and is not retained by us. All other features work entirely without AI.
- Using the **Action Market**: it only downloads JSON configuration (actions / prompts and other pure data) from the catalog URL you subscribe to; it uploads no local information.

## Local storage

The following is stored only in your browser locally (`chrome.storage` for the extension, GM storage for the userscript):

- Toolbox configuration (modes / scenes / actions / extraction rules / preferences)
- Connection info and secrets (note-service tokens; the config file stores only references, secrets are stored separately)
- Local scripts (the extraction functions you write yourself)
- Action usage records (click counts / success or failure / duration; no page content, clearable in one click on the "Runs" page)
- Browsing footprint (time on page / site / recent visits; on by default, can be turned off or cleared anytime under "Browsing footprint" on the "Runs" page)

Clearing the extension data or the userscript storage removes them.

## What the permissions are for

- `storage`: to save the configuration and secrets above.
- Site access (`host permissions` / `*://*/*`): to show the floating orb on web pages and read the current page's content according to your actions.
- `downloads` (extension): only for "save locally" — when you actively click a save-type action, it writes the file generated in that run (Markdown / text / images) to your Downloads folder; it does not read, list, or manage your existing downloads.
- `userScripts` (extension): to run the "local scripts" you write yourself; when not enabled, the feature only shows a hint.
- **Userscript**: it does not use the extension permissions above; instead the userscript manager provides equivalent APIs (GM storage / clipboard / cross-origin requests / notifications / open tab). The manager shows you that grant list at install time.

## Chrome Web Store data-usage declaration

**The only category involved: Website content.**

- **Website content**: the extension reads the visible text / image URLs / links of **only the current page**, and only when **you trigger an action** (by clicking, or when you have enabled "auto-run" for that action), to produce the result you configured (copy to clipboard, write to your own notes, render a share card). Auto-run is off by default, enabled per action, and runs only on matching pages that are currently open — no background bulk collection; sites listed as "quiet" never trigger. Among these, "write to notes" and "AI extraction" send content to **a service you configure yourself** (Orca Note / SiYuan kernel / your model endpoint) — it does not pass through us, and we have no server that could receive it; "save to Obsidian" instead hands content to the Obsidian app on your machine, so it never leaves your device. Cover images and the like are fetched from the relevant image host only when you generate a share card.

**No other category is involved, item by item:**

- **Browsing history**: the extension reads the single page you actively act on, only to show the orb and actions; there is also a **local browsing footprint** (time on page / site / recent visits), on by default, stored only on your machine, never uploaded or exported, and can be turned off or cleared anytime under "Browsing footprint" on the "Runs" page.
- **User activity**: no network monitoring on pages. Only when you explicitly configure "web operations" such as "click / fill" in an action will the extension dispatch synthetic events (ordinary clicks / input, not background monitoring or rewriting of your actions) to the current page per your configuration; the action usage records on the "Runs" page count only the trigger count / success or failure / duration of **this extension's actions**, stored locally, with no page content, clearable in one click, and never exported.
- **Authentication information**: note-service tokens / model API keys are entered by you and stored only on your machine (exported config files **do not contain secrets**), and are used only to access the service you configured.
- **Personally identifiable information / health / financial and payment info / personal communications / location**: not read, stored, or uploaded.

Shunshou contains no analytics, advertising, or crash-reporting SDK; apart from the actions you trigger and the "Check for updates" you click manually, it makes no network requests on its own.

## Third parties

Shunshou bundles no analytics, advertising, or crash-reporting SDK; the action usage records on the "Runs" page are stored locally and never uploaded. Except for actions you actively trigger and the manual "Check for updates" (which requests only public release info from GitHub Releases), it makes no network requests.

## Contact

Questions? Please use [Issues](https://github.com/hqweay/shunshou/issues).
