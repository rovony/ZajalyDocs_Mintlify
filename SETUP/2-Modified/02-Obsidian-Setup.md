---
title: Obsidian Setup — Complete Guide
type: guide
status: published
owner: Malek
tags: [setup, obsidian, sync, publish, plugins]
project: general
version: 1.1
created: 2026-02-19
updated: 2026-02-19
publish: false
---

# Obsidian Setup — Complete Guide

> One vault at root. Hidden system folders. $4/mo Sync across devices. $8/mo Publish to `vault.zajaly.dev` with password protection.

---

## Why One Vault at Root

Your Obsidian vault opens at `C:\Zajaly\ZajalyDocs` — the entire repo root, not a subfolder.

**Why not separate vaults per folder?**

| Approach | Wikilinks across folders? | Dataview across folders? | Sync cost | Verdict |
|---|---|---|---|---|
| 1 vault at root | ✅ Yes | ✅ Yes | $4/mo (one vault) | ✅ **Use this** |
| 1 vault per folder | ❌ No — vaults are isolated | ❌ No | $12+/mo (3+ vaults) | ❌ Expensive, fragmented |
| Vault on ZajDocs/ only | ✅ Within ZajDocs | ✅ Within ZajDocs | $4/mo | ❌ Can't link to ZajProjects/ |

The root vault lets you link a server guide in `ZajDocs/Guides/Servers/` directly to Custojo deployment notes in `ZajProjects/Custojo/` — that cross-pollination is the whole point of a knowledge base.

**What about clutter?** System folders (`_Admin`, `_Inbox`, `_Sources`) are hidden from Obsidian's sidebar (Step 2 below). You only see your three Zaj folders.

**What about Publish leaking private files?** Obsidian Publish only publishes files you explicitly select AND that have `publish: true` in frontmatter. Double gate. Nothing leaks.

---

## Step 1 — Install Obsidian

1. Go to **https://obsidian.md** → Download for Windows
2. Run installer, launch Obsidian
3. When asked → **Open folder as vault** → select `C:\Zajaly\ZajalyDocs`
4. Obsidian creates a `.obsidian/` config folder inside your repo (already in `.gitignore` selectively)

> [!NOTE]
> If you previously opened a subfolder (like the old `ZajDocs/`) as the vault, close that vault first (Settings → Switch vault → Remove), then re-open at root.

---

## Step 2 — Hide System Folders

After opening the vault, you'll see all six root folders in the sidebar. The three `_` folders are system/support — you rarely need them in Obsidian. Hide them so your sidebar only shows `ZajContent`, `ZajDocs`, `ZajProjects`.

### Method A — Obsidian's Built-in Excluded Files (recommended)

1. **Settings → Files & Links**
2. Scroll to **Excluded files** (text field at the bottom)
3. Add these patterns, one per line:

```
_Admin
_Inbox
_Sources
```

4. Close settings → the three folders vanish from the sidebar immediately
5. They still exist on disk, still sync via Git, still accessible via Quick Switcher (Ctrl+O) — just hidden from the file tree

> [!TIP]
> If you ever need to browse a hidden folder, temporarily remove it from the Excluded files list, or use Quick Switcher to jump directly to any file by name.

### Method B — File Hider Plugin (toggle on/off with hotkey)

If you want a quicker way to show/hide folders without editing settings:

1. Install **File Hider** from community plugins
2. In the sidebar, right-click `_Admin` → **Toggle file visibility**
3. Repeat for `_Inbox` and `_Sources`
4. Hidden folders show a 🚫 icon when File Hider's "show hidden" is active
5. Set a hotkey: Settings → Hotkeys → search "File Hider" → assign `Ctrl+Shift+H` to "Toggle hidden files visibility"

Now `Ctrl+Shift+H` instantly shows/hides all system folders when you need them.

### Method C — Both (belt and suspenders)

Use the built-in Excluded files for the permanent hide, AND install File Hider for temporary access. They don't conflict.

### After Hiding — Your Sidebar

```
ZajalyDocs (vault root)
├── ZajContent/          ← Blog drafts + course scripts
├── ZajDocs/             ← Guides, tools, essentials (→ GitBook)
└── ZajProjects/         ← Per-product docs (→ GitBook per product)
```

Clean. Three folders. Everything you work on daily.

> [!IMPORTANT]
> **Hidden ≠ deleted.** Hidden folders are fully functional — Git tracks them, Obsidian Sync syncs them, Dataview can query into them, and wikilinks to files inside them still work. They're just not cluttering your sidebar.

---

## Step 3 — Configure Settings

### Editor (Settings → Editor)

| Setting | Value | Why |
|---|---|---|
| Default editing mode | **Source mode** | See raw markdown, no surprises |
| Show line numbers | ON | Easier reference when editing |
| Spellcheck | ON | Catch typos |
| Readable line length | ON | Limits line width for readability |
| Show frontmatter | ON | Always see your YAML metadata |
| Strict line breaks | OFF | Standard markdown behavior |
| Fold heading | ON | Collapse sections while working |
| Fold indent | ON | Collapse nested content |

### Files & Links (Settings → Files & Links)

| Setting | Value | Why |
|---|---|---|
| Default location for new notes | **Same folder as current file** | Notes stay organized where you create them |
| New link format | **Shortest path when possible** | Cleaner wikilinks |
| Use `[[Wikilinks]]` | ON | Obsidian's native linking |
| Automatically update internal links | ON | Rename a file → all links update |
| Detect all file extensions | ON | See non-markdown files too |
| Default location for attachments | **In subfolder under current folder** | Name the subfolder `_assets` |
| Attachment subfolder name | `_assets` | Images/files stay with their notes |
| Excluded files | `_Admin`, `_Inbox`, `_Sources` | Hide system folders (Step 2) |

### Appearance (Settings → Appearance)

1. Base theme → **Dark**
2. Browse themes → install **Minimal** → activate it
3. Install **Style Settings** plugin (see Step 4) to customize Minimal

### Hotkeys (Settings → Hotkeys)

| Action | Hotkey |
|---|---|
| Quick switcher: Open | `Ctrl+O` (default) |
| Command palette | `Ctrl+P` (default) |
| Toggle edit/preview mode | `Ctrl+E` (default) |
| Insert template (Templater) | `Alt+T` |
| Search | `Ctrl+Shift+F` (default) |
| Create new note | `Ctrl+N` (default) |
| Open Graph View | `Ctrl+G` |
| Toggle hidden files (File Hider) | `Ctrl+Shift+H` |

---

## Step 4 — Install Plugins

### Core Plugins (Settings → Core plugins → toggle ON)

Enable these built-in plugins:
- **Templates** — basic template insertion
- **Tags view** — browse all tags in sidebar
- **Backlinks** — see what links TO the current note
- **Outline** — heading-based navigation panel
- **Word count** — status bar word/character count
- **Page preview** — hover over links to preview
- **Search** — vault-wide search
- **Quick switcher** — fuzzy-find any note by name (reaches hidden folders too)
- **Starred/Bookmarks** — pin frequently used notes
- **Slash commands** — type `/` for quick actions

### Community Plugins

**Settings → Community plugins → Turn off restricted mode → Browse**

Install these in order:

#### 4A — File Hider (sidebar cleanup)

Install first so you can immediately hide system folders.

1. Install **File Hider** from community plugins
2. Right-click `_Admin`, `_Inbox`, `_Sources` → **Toggle file visibility**
3. Set hotkey: `Ctrl+Shift+H` for toggle

#### 4B — Obsidian Git (backup to GitHub)

| Setting | Value |
|---|---|
| Vault backup interval (minutes) | **30** |
| Auto pull on startup | ON |
| Commit message | `vault backup: {{date}}` |
| Push on backup | ON |
| Pull updates on startup | ON |

**How it works:** Every 30 minutes, Obsidian Git commits all changes and pushes to `github.com/rovony/ZajalyDocs`. On startup, it pulls any changes (e.g., from GitBook edits or Cursor edits). This runs alongside Obsidian Sync — they serve different purposes.

> [!IMPORTANT]
> **Git vs Sync — no conflict:** Git creates versioned snapshots on GitHub. Sync streams changes instantly between devices. They operate on different layers and don't interfere with each other.

#### 4C — Dataview (query engine)

| Setting | Value |
|---|---|
| Enable JavaScript queries | ON |
| Enable inline queries | ON |

**Example queries you'll use:**

All published guides:
````markdown
```dataview
TABLE status, tags, updated
FROM "ZajDocs/Guides"
WHERE type = "guide" AND status = "published"
SORT updated DESC
```
````

Everything about a specific project:
````markdown
```dataview
TABLE title, type, status
FROM ""
WHERE project = "custojo"
SORT updated DESC
```
````

All outdated content needing review:
````markdown
```dataview
TABLE title, file.folder
FROM ""
WHERE status = "outdated"
SORT file.folder ASC
```
````

#### 4D — Templater (advanced templates)

| Setting | Value |
|---|---|
| Template folder location | `ZajDocs/Defaults/Templates` |
| Trigger Templater on new file creation | ON |
| Enable system commands | OFF (security) |

**Templates already created in your vault:**
- `Guide-Template.md` — tech guides and SOPs
- `SOP-Template.md` — standard operating procedures
- `Tool-Review-Template.md` — tool evaluations
- `Comparison-Template.md` — side-by-side comparisons
- `Course-Lesson-Template.md` — Skillplate lesson scripts
- `Blog-Post-Template.md` — Hashnode article drafts
- `Topic-Research-Template.md` — research capture

**Using templates:** In any folder, press `Alt+T` → select template → it inserts with auto-filled date and cursor placement.

#### 4E — Other Essential Plugins

| Plugin | Purpose | Key Config |
|---|---|---|
| **Calendar** | Daily/weekly notes sidebar | Default settings |
| **Folder Note** | Auto-creates summary note when you click a folder | Note name: folder name |
| **Style Settings** | Fine-tune Minimal theme (colors, fonts, density) | Accessible after Minimal installed |
| **Tag Wrangler** | Right-click tags to rename/merge across entire vault | Default settings |
| **Linter** | Auto-format markdown on save | Enable: YAML sort, heading blank lines, trailing spaces |
| **Iconize** | Add icons to folders in sidebar | Use to visually distinguish ZajDocs/ZajContent/ZajProjects |
| **Various Complements** | Auto-complete for wikilinks and tags | Default settings |

#### Iconize Setup (visual folder distinction)

1. Install Iconize from community plugins
2. Right-click each folder in sidebar → **Change icon**
3. Suggested icons:
   - `ZajContent` → ✏️
   - `ZajDocs` → 📖
   - `ZajProjects` → 🚀

This gives you instant visual distinction in the sidebar.

---

## Step 5 — Obsidian Sync ($4/mo)

Sync keeps your vault identical across all devices in real-time.

### 5A — Purchase

1. Go to **https://obsidian.md/account** → sign in (or create account)
2. Go to **https://obsidian.md/pricing** → purchase **Sync Standard**
   - $4/mo billed annually ($48/year)
   - $5/mo billed monthly
3. Sync activates immediately on your account

### 5B — Connect on Primary Device (PC)

1. In Obsidian: **Settings → Sync** → Log in with your Obsidian account
2. Click **Create new remote vault** → name it `ZajalyDocs`
3. Set encryption password (remember this — you'll need it on every device)
4. Click **Create**
5. Toggle Sync ON

### 5C — What to Sync

| Item | Sync? | Why |
|---|---|---|
| All markdown files | ✅ Yes | Your content |
| `_assets/` folders | ✅ Yes | Images and attachments |
| `.obsidian/plugins/` | ✅ Yes | Same plugins everywhere |
| `.obsidian/themes/` | ✅ Yes | Same appearance |
| `.obsidian/snippets/` | ✅ Yes | Custom CSS |
| `.obsidian/workspace.json` | ❌ No | Device-specific layout |
| `.obsidian/workspace-mobile.json` | ❌ No | Device-specific |

In Sync settings → **Selective sync** → exclude:
- `.obsidian/workspace.json`
- `.obsidian/workspace-mobile.json`

### 5D — Connect on Mobile / Other Devices

1. Install Obsidian on device (iOS, Android, Mac, Linux)
2. Open Obsidian → **Set up Sync** (don't create a new vault)
3. Log in → select `ZajalyDocs` remote vault
4. Enter encryption password
5. Choose a local folder for the vault
6. Wait for initial sync (may take a few minutes depending on vault size)

> [!TIP]
> Hidden folder settings (from Step 2) sync via `.obsidian/app.json`, so your mobile device will also have the clean three-folder sidebar automatically.

### 5E — Sync Limits (Standard Plan)

| Limit | Value |
|---|---|
| Storage per vault | 10 GB |
| Max file size | 200 MB |
| Version history | 12 months |
| Devices | Unlimited |
| Vaults | 1 (Standard) or 10 (Plus) |

10 GB is plenty for a text-heavy vault. If you add many large images or PDFs, consider keeping those in `_Sources/` and excluding that folder from Sync (access via Git instead).

---

## Step 6 — Obsidian Publish ($8/mo)

Publish turns selected notes into a public (or password-protected) website.

### 6A — Purchase

1. Go to **https://obsidian.md/pricing** → purchase **Publish**
   - $8/mo billed annually ($96/year)
   - $10/mo billed monthly
2. Activates immediately

### 6B — First Publish

1. In Obsidian: click the **Publish** icon (paper plane ✈️) in the left ribbon
2. You'll see all vault files listed
3. Check the files you want to publish — **only files with `publish: true` in frontmatter should be selected**
4. Click **Publish**
5. Your site is live at `publish.obsidian.md/your-site-id`

### 6C — Custom Domain (`vault.zajaly.dev`)

1. In Obsidian Publish settings → **Manage sites** → your site → **Custom domain**
2. Enter: `vault.zajaly.dev`
3. In Cloudflare DNS for `zajaly.dev`:

| Type | Name | Target | Proxy |
|---|---|---|---|
| CNAME | `vault` | `publish-main.obsidian.md` | **DNS only** (gray cloud) |

4. Wait 15-60 min for DNS propagation
5. Back in Obsidian → click **Verify** → should confirm

> [!CAUTION]
> **Must be DNS only (gray cloud), NOT proxied (orange cloud).** Obsidian Publish doesn't work behind Cloudflare's proxy because it needs its own SSL certificate negotiation.

### 6D — Password Protection

1. Publish settings → **Site options** → **Password**
2. Set a password
3. All visitors must enter the password to see ANY published page

**Limitation:** Site-wide only. Cannot password-protect individual pages. Everything published is behind one password, or nothing is.

**Strategy:** Use password protection for your private knowledge base. Public-facing product docs go on GitBook instead.

### 6E — Publish Filtering Strategy

Your vault has 6 root folders. Here's what should and shouldn't be published:

| Folder | Publish to Obsidian? | Why |
|---|---|---|
| `_Admin/` | ❌ Never | Internal system files (hidden in sidebar) |
| `_Inbox/` | ❌ Never | Raw captures (hidden in sidebar) |
| `_Sources/` | ❌ Never | External reference material (hidden in sidebar) |
| `ZajContent/` | ❌ Never | Goes to Hashnode/Skillplate instead |
| `ZajDocs/` | ✅ Selectively | Guides + tools you want on your private site |
| `ZajProjects/` | ⚠️ Maybe | Internal project notes yes, customer-facing → GitBook |

**How to control it:**

1. **Frontmatter gate:** Only files with `publish: true` appear in the Publish dialog
2. **Manual selection:** You still choose which `publish: true` files to actually push live
3. **Bulk ignore:** Folders where NO files have `publish: true` are invisible to Publish

**Recommended frontmatter per folder:**

```yaml
# _Admin/, _Inbox/, _Sources/, ZajContent/ files:
publish: false    # Always false — never candidates

# ZajDocs/ files you want published:
publish: true     # Shows up in Publish dialog

# ZajDocs/ drafts or internal notes:
publish: false    # Won't appear in Publish dialog

# ZajProjects/ internal notes:
publish: true     # Your private reference (behind password)

# ZajProjects/ customer-facing docs:
publish: false    # These go to GitBook, not Obsidian Publish
```

### 6F — Site Appearance

Configure in Publish settings → **Site options**:

| Option | Recommended |
|---|---|
| Show graph view | ON — visual navigation for readers |
| Show navigation sidebar | ON |
| Show search | ON |
| Show backlinks | ON — shows connections between notes |
| Theme | Matches your vault theme |
| Custom CSS | Optional — paste CSS to brand the site |

### 6G — Publishing Workflow

**Day-to-day:**

1. Write or update a note in Obsidian
2. Set `publish: true` in frontmatter (if not already)
3. Click Publish icon (✈️) → you'll see changed files highlighted
4. Select what to push → **Publish**
5. Live within seconds at `vault.zajaly.dev`

**Unpublishing:** Uncheck a file in the Publish dialog → click **Publish** → removed from site but stays in vault.

---

## Step 7 — Vault Dashboard

Create a dashboard note at the vault root for quick navigation.

**Create `C:\Zajaly\ZajalyDocs\Dashboard.md`:**

```markdown
---
title: Dashboard
type: reference
status: published
owner: Malek
tags: [dashboard, index]
project: general
publish: false
---

# 🏠 ZajalyDocs Dashboard

## 📊 Vault Stats
```

````markdown
```dataview
TABLE length(rows) as "Count"
FROM ""
WHERE type
GROUP BY type
```
````

```markdown
## 📝 Recently Updated
```

````markdown
```dataview
TABLE status, project, file.folder as "Location"
FROM ""
WHERE type
SORT file.mtime DESC
LIMIT 15
```
````

```markdown
## ⚠️ Needs Attention
```

````markdown
```dataview
TABLE type, file.folder as "Location"
FROM ""
WHERE status = "draft" OR status = "outdated"
SORT status ASC
```
````

```markdown
## 🔗 Quick Links

- [[ZajDocs/Guides/Servers/README|Server Guides]]
- [[ZajDocs/Guides/Laravel/README|Laravel Guides]]
- [[ZajDocs/Tools/README|Tool Reviews]]
- [[ZajProjects/Custojo/README|Custojo Docs]]
- [[ZajProjects/Waraq/README|Waraq Docs]]
- [[ZajContent/Blog/README|Blog Drafts]]
- [[ZajContent/Courses/README|Course Scripts]]
```

> [!TIP]
> Star/bookmark this Dashboard note for one-click access from any device.

---

## Step 8 — Verify Everything Works

### Vault

- [ ] Obsidian opens at `C:\Zajaly\ZajalyDocs` (root, not a subfolder)
- [ ] Only 3 folders visible in sidebar: `ZajContent`, `ZajDocs`, `ZajProjects`
- [ ] `_Admin`, `_Inbox`, `_Sources` are hidden (not visible in sidebar)
- [ ] Quick Switcher (Ctrl+O) can still find files in hidden folders
- [ ] Minimal theme active, dark mode
- [ ] Wikilinks work (create a test link from ZajDocs/ to ZajProjects/)
- [ ] Frontmatter visible on all files

### Plugins

- [ ] File Hider: `Ctrl+Shift+H` toggles hidden folders visibility
- [ ] Obsidian Git: committed and pushed in last 30 min (check status bar)
- [ ] Dataview: run a test query (open Dashboard, see results)
- [ ] Templater: press `Alt+T` in any folder, see template list from `ZajDocs/Defaults/Templates`
- [ ] Iconize: folder icons visible (📖 ZajDocs, ✏️ ZajContent, 🚀 ZajProjects)
- [ ] Linter: save a file, see it auto-format

### Sync

- [ ] Obsidian Sync connected (Settings → Sync → status shows "Connected")
- [ ] Open vault on phone/tablet — same content appears
- [ ] Hidden folder settings transferred to mobile (same clean sidebar)
- [ ] Edit on phone → appears on PC within seconds
- [ ] `workspace.json` NOT syncing (check Sync settings)

### Publish

- [ ] At least one test file has `publish: true`
- [ ] Click Publish icon → file appears in dialog
- [ ] Published → visible at `vault.zajaly.dev`
- [ ] Password works (visit in incognito, must enter password)
- [ ] Files with `publish: false` do NOT appear in Publish dialog
- [ ] Files in `_Admin/`, `_Inbox/`, `_Sources/` never appear in Publish dialog

### Git

- [ ] `github.com/rovony/ZajalyDocs` has recent commits from Obsidian Git
- [ ] `.obsidian/workspace.json` is NOT in the repo (check `.gitignore`)
- [ ] Hidden folders (`_Admin`, etc.) ARE in the repo (hiding is Obsidian-only, Git tracks everything)

---

## Troubleshooting

### Hidden folders aren't hiding
**Check:** Settings → Files & Links → Excluded files → are the patterns listed?
**Alternative:** Use File Hider plugin instead (right-click → Toggle visibility).

### Quick Switcher can't find files in hidden folders
**Check:** Quick Switcher should find ALL files regardless of hiding. If it doesn't, the Excluded files setting may be too broad.
**Fix:** Make sure you're excluding folder names (`_Admin`) not wildcards (`_*`).

### Obsidian Git won't push
**Check:** Is Git installed on your system? Obsidian Git requires Git CLI.
**Fix:** Install Git for Windows from `https://git-scm.com`. Restart Obsidian.

### Sync conflict — file has both local and remote changes
**How it works:** Obsidian Sync creates a conflict file (e.g., `note (conflict).md`). It never overwrites.
**Fix:** Open both versions, manually merge, delete the conflict copy.

### Publish shows "custom domain not verified"
**Check:** Is the Cloudflare CNAME set to DNS only (gray cloud)?
**Fix:** Turn OFF Cloudflare proxy (orange → gray cloud). Wait 30 min. Re-verify.

### Dataview queries show nothing
**Check:** Do your files have frontmatter? Dataview needs `type`, `status`, etc. in YAML.
**Fix:** Add frontmatter to files. Run "Dataview: Rebuild index" from command palette.

### Template folder empty in Templater
**Check:** Is `ZajDocs/Defaults/Templates` the folder set in Templater settings?
**Fix:** Settings → Templater → Template folder location → browse to correct path.

### Git and Sync both running — will they conflict?
**No.** Git works on files (snapshots to GitHub). Sync works on files too but streams them live between devices. They read the same files but don't interfere. The only edge case: if you edit the same file simultaneously on two devices while offline — Sync handles this with conflict resolution.

---

*Save to: C:\Zajaly\ZajalyDocs\_Admin\Setup\02-Obsidian-Setup.md*
*Version: 1.1 — February 19, 2026*
*Changes: Folders renamed to ZajDocs/ZajContent/ZajProjects. Folder hiding fully documented (3 methods). All paths updated.*
