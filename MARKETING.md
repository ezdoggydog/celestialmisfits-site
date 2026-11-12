# Marketing and SEO: where this stands

_Nov 12, 2026._

## What the site is for

**Discovery and conversion are different jobs, and this site only does one of them.**

Rust players find servers in the **in-game server browser**, on **BattleMetrics**, on trackers like
**just-wiped.com**, in **Discord**, and by word of mouth. Almost nobody finds a Rust server by
searching Google. So the site's job is **conversion**: somebody hears the name, looks it up, and
decides whether to join.

That is worth doing well, and it is what the November 12 work improved. It is not a traffic
strategy, and no amount of SEO will make it one.

The thing this server has that almost no other server has: it is **veteran-run and
veteran-friendly**, with a real nonprofit behind it (214 Life) and a crisis page that is not
marketing. That travels in places advertising does not reach.

## Done (Nov 12, 2026)

From a SearchFit `/seo-check` handoff, home page scoring 55/100.

- **Home page**: the approved head block (title 17 → 52 characters and now carries the keyword),
  description rewritten with PvE, veteran-friendly and a call to action, canonical, Open Graph,
  Twitter card, and `theme-color` set to the real `--sky` background `#0a1028` rather than left as
  a placeholder. JSON-LD (WebSite + Organization) with the Discord invite and 214life.org in
  `sameAs`. Real pixel dimensions on the two images that were causing layout shift.
- **All 18 other pages**: canonical, OG, Twitter card, theme-color. Titles keep their own voice and
  gain the keyword -- "Halloween on Celestial Misfits | Rust PvE Server", not the handoff's
  product-listing pattern. Descriptions went from an 84-115 character template to 127-147
  characters saying what is actually on the page. `og:image` is each season's own banner.
- **Three pages are deliberately not written as fun**: Memorial Day, the Marine Corps Birthday and
  Veterans Day get plain, respectful descriptions and lead with veteran-friendly, not with the joke.
- **help.html is a crisis page.** Correct basic tags, a factual description naming 988, the Veterans
  Crisis Line and `/lifeline`, and deliberately **no `og:image`** and only a summary card -- a
  cartoon bloodhound beside a suicide-prevention link in a Discord preview is the wrong note. Its
  wording is untouched and should stay that way.
- **sitemap.xml and robots.txt**, which the handoff only suggested considering.
- **The JavaScript problem, which was the real find.** Three things that matter were invisible to
  anything that does not run scripts: the Discord button, the Donate button (both `href="#"`) and
  the server address, which said "Server address coming soon" in the markup while
  `CONFIG.serverAddress` was already `play.celestialmisfits.com`. Google's snippet, Discord link
  previews and anyone with JS blocked saw a server with no address and two dead buttons. All three
  are in the HTML now; the JS still writes the same values, so nothing changed for a normal visitor.

Check after a deploy: `curl -s https://celestialmisfits.com/ | grep -E 'addr|discord.gg'`

## Plugins

Four installed, all four worth keeping:

| Plugin | Use it for |
|---|---|
| **SearchFit SEO** | site audits, schema, keyword work |
| **Postclick: Landing Page CRO** | what stops a visitor joining. Found the server-address bug. |
| **Marketing** (Anthropic) | three of its eight skills: `competitive-brief`, `campaign-plan`, `brand-review` |
| **Postiz** | scheduling posts. **Not set up -- see below.** |

Skip from the catalog: Windsor.ai, Supermetrics, Trackian, Hyper, dataslayer (all ad-platform
reporting, and there is no ad spend to report on), Marketing for Life Sciences (pharma), and the
duplicate SearchFit SEO listing. **Social Media Skills** (106 skills, community-authored) is the
only other real candidate, and only once there is a posting habit to support.

Of the Marketing skills, skip `email-sequence` (no mailing list), `performance-report` (no data
yet) and `seo-audit` (SearchFit covers it).

## Roadmap

### Postiz -- on hold, Nov 12 2026

MoonDoggy: "let's hold off on postiz for a bit, but keep it in the roadmap."

**Set it up when there is a reason to post on a rhythm** -- wipe announcements, season launches,
the Veterans Day parade. The material is already good; the habit is the missing part.

**The gate he set (Nov 12 2026):** "I think we will go there eventually with Postiz. But I want to
have the first couple of months of the storyline (with appropriate maps) generated before
committing funding for that ($29/month)." Right order -- there is nothing worth announcing until
there is something to announce, and paying to schedule posts about content that does not exist yet
is backwards.

Which makes the real blocker the Grimwood Saga, not the marketing. **Chapter 1 has never been
walked end to end.** On Nov 11 we found that BasePlayer.userID is an EncryptedValue<ulong> struct,
so Dialogs' conditioned nodes silently read false and only nodes with NO conditions could ever
fire -- every conditioned node in the saga had been unreachable since it was written. The fix is
in (third-party/PlayerEventStates.cs patched, /story probe and /story chapter1 built to verify
it), but the verification has not been run on the server yet. That comes first.

Steps when the time comes:

1. **His**: an account at postiz.com (or self-host; it is open source), then connect the channels.
   That is OAuth in a browser, so it cannot be done from a Claude session.
2. **His**: generate an API key in Postiz settings.
3. **Mine**: `npm install -g postiz`, then use it.

Two things to know before starting:

- `postiz auth:login` is a browser device flow that **cannot** be completed from the container, so
  it has to be the API key route.
- The container is ephemeral, so the key does not survive between sessions and has to be pasted
  each time. Per his standing rule it is exported in-session only -- never echoed, never written
  into a repo, never committed.

**And the question to answer first: what gets posted, and where?** If the answer is mostly Discord,
Postiz is not needed -- a Discord webhook does that with no account and nothing to re-auth.
**Postiz earns its keep for Reddit**, because r/playrust is the one channel that could bring in
people who have never heard of the server.

### Still open

- A full `/searchfit-seo:seo-audit` across the site (broken links, deeper technical checks).
- `marketing:competitive-brief` against other Rust PvE servers -- which angles nobody has claimed.
- The things that actually drive discovery, none of which are this website: the server browser
  description and tags, BattleMetrics presence, and wipe announcements where Rust players look.

## Video (Nov 12, 2026)

`videos.html` is the preview page. Thumbnails are YouTube's own and the player is only fetched
when somebody clicks one, so a page of a dozen clips loads like a page of a dozen images.
Add a clip by putting its YouTube ID in the `CLIPS` list in that page; an entry with no ID is
skipped, so the list doubles as the shot list.

**Host on YouTube, not here.** This repo is GitHub Pages: a 100 MB hard limit per file, a 1 GB
soft limit on the repo, and 100 GB/month of bandwidth shared across the whole site. One 4K clip
is 116 MB on its own. YouTube is free, has no limit, and is itself the second-biggest search
engine — a clip titled "Rust PvE server traffic system" is discovery we are not otherwise
paying for. Make them public rather than unlisted for that reason.

**Capture settings.** NVIDIA in-game capture was recording 4K at 120 fps, 62 Mbps: 116 MB for
fifteen seconds. 1080p60 at 20-30 Mbps is the right setting for anything headed to the web, and
re-encoding that same clip to 1080p60 brought it to 18 MB with no visible loss at the size
anyone will watch it.

### What to show, in order of what nobody else has

1. **Traffic on the ring road.** Rigs, trailers, a city bus that stops at the stops. No other
   Rust server has moving road traffic. Lead with it.
2. **Cruise control steering itself.** Hands off the wheel through a bend, braking for the
   truck ahead. This reads as impossible to anyone who plays Rust, which is exactly why it
   works as the thing people send each other.
3. **The sky crane with a slung load.** A crate on a line under the hook, crossing the island.
4. **The Veterans Day parade.** 22 vehicles, police escorts, an F-16 pass every minute. This is
   the one that says what kind of server this is, not just what it can do.
5. **Grimwood after dark.** Atmosphere only -- the town, the fog, the people. Nothing of the
   story. The saga stays unspoilt.
6. **The Headless Horseman**, once October comes round again.

Keep each one 15-30 seconds and start on motion: no slow pans in, no title cards. Nothing
needs music, and anything with music is a copyright claim waiting to happen on a channel we
want to keep.

**Channel:** https://www.youtube.com/@CelestialMisfits (created Nov 12, 2026; handle claimed
the same day). The channel-ID URL `youtube.com/channel/UC_wsBd4SFKASrz_VlPHt6UQ` still works
and is permanent -- worth keeping somewhere, since a handle can be changed or lost and that
one cannot.
It is listed in the site footer and in the homepage's JSON-LD `sameAs`, which is how a search
engine learns the channel and the server are the same outfit.

Banner and watermark built Nov 12 and kept in the repo under `img/`: `yt_banner.jpg`
(2560x1440, logo inside the 1546x423 phone-safe strip) and `yt_watermark.png` (150x150, the
hound alone -- the wordmark is unreadable at that size).
