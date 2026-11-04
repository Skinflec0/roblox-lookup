# Roblox Lookup

A single-page tool for looking up public Roblox users, groups, experiences (games) and catalog items by name, ID or pasted link. It also does bulk lookups, side-by-side user comparisons and random discovery. No backend, no build step, one HTML file.

## Features

**Six search types**

| Type | What you get |
| --- | --- |
| **User** | Overview and stats, past usernames, creations, favorites, groups, friends, followers, following, avatar and outfits, currently worn items, limiteds with estimated RAP, badges, linked social accounts, live presence |
| **Group** | Overview and shout, roles with member shares, members, games, wall posts, allies, enemies, name history, social links |
| **Game** | Details and vote ratio, media, running servers, places, game passes, badges, recommended games, social links |
| **Asset** | Details, resale data and resellers, price and volume history charts, owners, bundles, recommended items |
| **Bulk users** | Look up to 100 usernames or IDs at once in a table; export CSV or JSON, copy as Markdown |
| **Compare users** | `userA vs userB` with followers, friends, limiteds, RAP, account age, presence and status |

**Search helpers**
- Search by name, numeric ID, or paste a link (roblox.com `users`, `groups`, `games`, `catalog`, `library`, `game-pass`, `bundles`, `outfits`, and Rolimons player and item links)
- Game search accepts either a universe ID or a place ID
- Type-ahead suggestions with thumbnails
- **Random** button for users, groups, assets and popular games
- Recent searches (last 12) and a watchlist (up to 40) for quick return

**Working with results**
- Filter and sort grids, load long lists in pages or **Load all**, and export lists as CSV
- Copy ID, copy summary, copy as Markdown, export JSON
- Screenshot of the result as a PNG (loads html2canvas from cdnjs the first time)
- Shareable links using the URL hash, for example `#user/1` or `#group/1`; the open tab is added to the link automatically as you switch tabs
- Interactive sparkline charts for resale history
- Print-friendly stylesheet

**Interface**
- Dark, light or auto theme, compact grid, optional sticky search bar
- Live presence refresh every 30 seconds
- Network health indicator and automatic retries with backoff on rate limits
- Built-in Terms of Use and Privacy Policy dialogs

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `/` or `Ctrl`/`Cmd` + `K` | Focus the search box |
| `Enter` | Search |
| `R` | Random |
| `1` to `6` | Switch type (User, Group, Game, Asset, Bulk, Compare) |
| `T` | Cycle theme |
| `?` | Show shortcuts |
| `Esc` | Close dialogs and suggestions |
| `↑` `↓` | Move through suggestions |

## Run locally

Open `index.html` in a browser, or serve the folder:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

1. Name the file `index.html` and commit it to the repo root.
2. In the repo, go to **Settings > Pages**.
3. Choose **Deploy from a branch**, select `main` and `/ (root)`, then save.
4. After a minute the site is live at `https://<your-username>.github.io/<repo>/`.

## How it gets data

Browsers cannot call most Roblox APIs directly because of CORS, so requests go through a public Roblox API proxy. Pick one in **Settings > Proxy host**:

| Host | Notes |
| --- | --- |
| `ff-roproxy.com` | Default |
| `roproxy.com` | Often unavailable |
| `roblox.com` | Direct, but limited by CORS; many calls are likely to fail from a web page |

If a request fails, the tool retries and then falls back to the other proxy. These proxies are third-party services run by other people. They can rate-limit, change or disappear, and when that happens lookups fail until you switch host or the service returns. If lookups stop working, check Settings first.

## Settings

Proxy host, theme, session response cache (5-minute TTL), remember recent searches, auto-load lazy tabs (followers, members), compact grid, sticky search, live presence refresh, concurrent request limit (2 to 20), clear cache, and wipe storage.

## Your data and privacy

- No account system, analytics, ads or cookies. Everything runs in your browser.
- `localStorage` (keys starting `rl_`) stores your theme, proxy choice, settings, recent searches and watchlist. **Settings > Wipe storage** removes it, and **Remember recent searches** can be turned off.
- Your searches are forwarded to the selected proxy and then to Roblox. Both may log requests under their own policies.
- Thumbnails load from Roblox's CDN, and the page loads Inter and JetBrains Mono from Google Fonts.

## Limitations

- **Public data only.** Roblox privacy settings can hide friends, followers, inventory, favorites, badges and more; those tabs show a note instead.
- **RAP is an estimate** calculated from each user's visible limited items. Do not use it for trading decisions.
- Some fields (owners, places, wall) need permissions the public API may not grant and can come back empty.
- Counts and prices can be stale or rate-limited. Large lists (followers, members, badges) load in pages of 100.
- Compare and bulk lookups make many requests; heavy use can trigger rate limits.

## Tech

Plain HTML, CSS and JavaScript. No framework, no build step. html2canvas is loaded from cdnjs only when you take a screenshot.

## Disclaimer

Not affiliated with, endorsed by or sponsored by Roblox Corporation. "Roblox" is a trademark of Roblox Corporation. Use the tool only for lawful, respectful purposes and follow the [Roblox Terms of Use](https://en.help.roblox.com/hc/en-us/articles/115004647846). Do not use it to harass people.
