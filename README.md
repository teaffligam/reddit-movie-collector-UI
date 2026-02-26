Features
🚫 Comment Hider & Blocklist
Add any movie title to your personal blocklist and comments mentioning it are automatically hidden. Tired of seeing Interstellar recommended in every thread? Gone. Your blocklist is fully yours — add titles one by one or bulk import/export as JSON. Supports any input format:
interstellar, the matrix, jaws
"Interstellar", "The Matrix", "Jaws"
["interstellar", "the matrix", "jaws"]
📊 Title Counter
Scans all visible comments and tallies which movies get mentioned most. A ranked list appears at the top of the thread so you can see what the crowd is actually recommending — not just what's loudest in the first few comments.
🖱️ Manual Collector
Click any comment to capture its movie title into a running list. Hit Copy when you're done to grab the whole thing as a clipboard-ready quoted list. Great for building a watchlist without switching tabs.
🎬 Movie Gallery (optional — requires free TMDB API key)
When enabled, inline poster cards appear beneath comments that mention films — showing the movie poster, TMDB rating, and release year. Click any card for a full detail popup:

Plot overview
Director + other films they've directed
Top cast with photos
Direct link to search on Letterboxd


Screenshots

Coming soon — feel free to add your own!


Installation

Install Tampermonkey for your browser
Click this link to the raw script — Tampermonkey will detect the .user.js and prompt you to install automatically
Click Install and you're done

Or install manually: open Tampermonkey → Dashboard → + → paste the script contents → Save.

Supported Subreddits
Subredditnew.redditold.redditr/horror✅✅r/movies✅✅r/MovieSuggestions✅✅r/horrorreviewed✅✅r/MovieRecommendations✅✅
Want another subreddit added? Open an issue or see Contributing.

TMDB API Key Setup
The Movie Gallery feature requires a free API key from The Movie Database. The key is stored locally in your browser and only used to make requests directly to TMDB — it is never sent anywhere else.
How to get your free key:

Create a free account at themoviedb.org
Go to Settings → API in your account menu
Click Create and choose Developer
Fill in the form (app name: anything, e.g. "Personal")
Copy the API Key (v3 auth) — it's a long hex string
In the floating panel on any supported Reddit thread, expand ⚙️ Settings → paste your key → click Save


Usage
Once installed, visit any supported subreddit thread. A floating 🎬 Movie Utilities panel will appear in the bottom-right corner.
ButtonWhat it does⟳ RecountRe-scan all comments and refresh the ranked list🎬 Gallery ON/OFFToggle inline movie poster cards⚙️ Settings ▼Expand to manage your API key, blocklist, and feature togglesCopyCopy your manually collected titles to clipboardClearClear the collector list
Click any comment (not on a button or card) to add its title to the collector. A green outline briefly flashes to confirm the capture.

How It Works
New Reddit vs Old Reddit
The script detects www.reddit.com vs old.reddit.com and uses a compatibility layer to handle both DOM structures. New Reddit uses custom elements like <shreddit-comment> while old Reddit uses .thing.comment. Both share the same logic.
TMDB Caching
Movie data is cached in localStorage for 7 days to avoid redundant API calls, using the key prefix rmu_tmdb2_.
Comment Hider
Comments are hidden by checking whether their text content includes any blocklist term (case-insensitive substring match). A MutationObserver handles dynamically loaded comments as you expand threads.
Gallery
An IntersectionObserver lazy-loads poster cards as comments scroll into view, staggering API calls by 150ms to stay well within TMDB's rate limits.

Privacy
This script collects no personal data.

Your blocklist, settings, and movie list are stored locally via Tampermonkey's GM_setValue
TMDB API calls go directly from your browser to api.themoviedb.org
Your API key is stored locally and never transmitted anywhere except TMDB
No analytics, no tracking, no external servers


Contributing
Pull requests are welcome. Some ideas:

 Add more subreddits (edit the @match lines in the userscript header)
 Improve movie title extraction accuracy
 Letterboxd watchlist export
 Screenshots for this README

To add a subreddit, add two new @match lines to the script header — one for www.reddit.com and one for old.reddit.com:
js// @match  https://www.reddit.com/r/YOURSUBREDDIT/comments/*
// @match  https://old.reddit.com/r/YOURSUBREDDIT/comments/*

