# 🎬 Reddit Movie Utilities

> Hide spoilers, count what's actually being recommended, collect titles, and browse inline TMDB posters — all inside Reddit movie threads.

A Tampermonkey userscript for anyone who regularly browses movie-focused subreddits.

---

## Features

### 🚫 Comment Hider & Blocklist
Add any movie title to your personal blocklist and comments mentioning it are automatically hidden. Tired of seeing *Interstellar* recommended in every thread? Gone. Your blocklist is fully yours — add titles one by one or bulk import/export as JSON. Supports any input format:

```
interstellar, the matrix, jaws
"Interstellar", "The Matrix", "Jaws"
["interstellar", "the matrix", "jaws"]
```

### 📊 Title Counter
Scans all visible comments and tallies which movies get mentioned most. A ranked list appears at the top of the thread so you can see what the crowd is actually recommending — not just what's loudest in the first few comments.

### 🖱️ Manual Collector
Click any comment to capture its movie title into a running list. Hit **Copy** when you're done to grab the whole thing as a clipboard-ready quoted list. Great for building a watchlist without switching tabs.

### 🎬 Movie Gallery *(optional — requires free TMDB API key)*
When enabled, inline poster cards appear beneath comments that mention films — showing the movie poster, TMDB rating, and release year. Click any card for a full detail popup:

- Plot overview
- Director + other films they've directed
- Top cast with photos
- Direct link to search on Letterboxd

---

## Screenshots

> *Coming soon — feel free to add your own!*

---

## Installation

Userscripts need a browser extension to run them. The two most popular options are **Tampermonkey** and **Violentmonkey** — both are free, both work with this script. Pick one.

---

### Step 1 — Install a userscript manager

**Google Chrome**
- [Tampermonkey for Chrome](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo) → click **Add to Chrome** → **Add extension**
- [Violentmonkey for Chrome](https://chrome.google.com/webstore/detail/violentmonkey/jinjaccalgkegedbjlghdfcdaenckbbf) → click **Add to Chrome** → **Add extension**

**Mozilla Firefox**
- [Tampermonkey for Firefox](https://addons.mozilla.org/en-US/firefox/addon/tampermonkey/) → click **Add to Firefox** → **Add**
- [Violentmonkey for Firefox](https://addons.mozilla.org/en-US/firefox/addon/violentmonkey/) → click **Add to Firefox** → **Add**

Once installed you'll see a small icon in your browser toolbar (a square with a checkmark for Tampermonkey, or a purple icon for Violentmonkey).

---

### Step 2 — Install the script

**Option A — One-click install (easiest)**

Click **[here to install the script](../../raw/main/reddit-movie-utils-tampermonkey.user.js)**. Your userscript manager will detect the file and show an install screen. Click **Install** and you're done.

**Option B — Copy & paste (if Option A doesn't work)**

1. Open the file [`reddit-movie-utils-tampermonkey.user.js`](../../blob/main/reddit-movie-utils-tampermonkey.user.js) in this repo
2. Click the **Raw** button (top-right of the file view) and select all the text (`Ctrl+A` / `Cmd+A`), then copy it (`Ctrl+C` / `Cmd+C`)
3. Click the userscript manager icon in your toolbar
4. **Tampermonkey:** click **Create a new script** — delete any placeholder text, paste yours in, then hit `Ctrl+S` / `Cmd+S` to save
5. **Violentmonkey:** click the **+** button → **New script** — delete the placeholder, paste, then click **Save**

---

### Step 3 — Verify it's working

Go to any supported Reddit thread (e.g. [r/horror](https://www.reddit.com/r/horror/) and open any post with comments). You should see the **🎬 Movie Utilities** panel appear in the bottom-right corner of the page within a couple of seconds.

If the panel doesn't appear, try refreshing the page. If it still doesn't show, check that the script is enabled in your userscript manager dashboard.

---

## Supported Subreddits

| Subreddit | new.reddit | old.reddit |
|---|---|---|
| r/horror | ✅ | ✅ |
| r/movies | ✅ | ✅ |
| r/MovieSuggestions | ✅ | ✅ |
| r/horrorreviewed | ✅ | ✅ |
| r/MovieRecommendations | ✅ | ✅ |

Want another subreddit added? Open an issue or see [Contributing](#contributing).

---

## TMDB API Key Setup

The Movie Gallery feature requires a free API key from [The Movie Database](https://www.themoviedb.org). The key is stored locally in your browser and only used to make requests directly to TMDB — it is never sent anywhere else.

**How to get your free key:**

1. Create a free account at [themoviedb.org](https://www.themoviedb.org/signup)
2. Go to **Settings → API** in your account menu
3. Click **Create** and choose **Developer**
4. Fill in the form (app name: anything, e.g. `"Personal"`)
5. Copy the **API Key (v3 auth)** — it's a long hex string
6. In the floating panel on any supported Reddit thread, expand **⚙️ Settings** → paste your key → click **Save**

---

## Usage

Once installed, visit any supported subreddit thread. A floating **🎬 Movie Utilities** panel will appear in the bottom-right corner.

| Button | What it does |
|---|---|
| **⟳ Recount** | Re-scan all comments and refresh the ranked list |
| **🎬 Gallery ON/OFF** | Toggle inline movie poster cards |
| **⚙️ Settings ▼** | Expand to manage your API key, blocklist, and feature toggles |
| **Copy** | Copy your manually collected titles to clipboard |
| **Clear** | Clear the collector list |

Click any comment (not on a button or card) to add its title to the collector. A green outline briefly flashes to confirm the capture.

---

## How It Works

### New Reddit vs Old Reddit
The script detects `www.reddit.com` vs `old.reddit.com` and uses a compatibility layer to handle both DOM structures. New Reddit uses custom elements like `<shreddit-comment>` while old Reddit uses `.thing.comment`. Both share the same logic.

### TMDB Caching
Movie data is cached in `localStorage` for 7 days to avoid redundant API calls, using the key prefix `rmu_tmdb2_`.

### Comment Hider
Comments are hidden by checking whether their text content includes any blocklist term (case-insensitive substring match). A MutationObserver handles dynamically loaded comments as you expand threads.

### Gallery
An IntersectionObserver lazy-loads poster cards as comments scroll into view, staggering API calls by 150ms to stay well within TMDB's rate limits.

---

## Privacy

This script collects **no personal data**.

- Your blocklist, settings, and movie list are stored locally via Tampermonkey's `GM_setValue`
- TMDB API calls go directly from your browser to `api.themoviedb.org`
- Your API key is stored locally and never transmitted anywhere except TMDB
- No analytics, no tracking, no external servers

---

## Contributing

Pull requests are welcome. Some ideas:

- [ ] Add more subreddits (edit the `@match` lines in the userscript header)
- [ ] Improve movie title extraction accuracy
- [ ] Letterboxd watchlist export
- [ ] Screenshots for this README

**To add a subreddit**, add two new `@match` lines to the script header — one for `www.reddit.com` and one for `old.reddit.com`:

```js
// @match  https://www.reddit.com/r/YOURSUBREDDIT/comments/*
// @match  https://old.reddit.com/r/YOURSUBREDDIT/comments/*
```

---

## License

MIT — do whatever you want with it.

---

## Acknowledgements

Movie data provided by [The Movie Database (TMDB)](https://www.themoviedb.org).
*This product uses the TMDB API but is not endorsed or certified by TMDB.*
