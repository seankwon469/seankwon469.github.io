# Donghyun Kwon — Personal Website

Personal academic website for **Donghyun Kwon**, Ph.D. Student at the Cho Chun Shik
Graduate School of Mobility, KAIST. Static site (HTML/CSS/JS).

## Structure

Multi-page static site, following the Academic Pages / Minimal Mistakes convention:
a masthead, a fixed author sidebar, and a reading column capped for measure.

```
site/
├── index.html            # About — bio and research interests
├── publications.html     # Journal articles, conference papers, awards
├── projects.html         # Research projects and their commissioning bodies
├── demo.html             # MATSim simulation clip
├── robots.txt            # Disallow all crawlers
├── README.md
└── assets/
    ├── css/style.css
    ├── js/main.js
    └── video/            # self-hosted demo clip + poster
```

Adding a page means copying the masthead/sidebar/footer shell from an existing
page and adding it to the nav list in all of them.

## Demo video

The demo clip is self-hosted rather than embedded from YouTube, so the page makes no
third-party requests. The 689 MiB source screen recording is re-encoded down to 21.5 MiB
so it stays well inside GitHub's file-size limits and downloads quickly:

```bash
ffmpeg -y -i source.mp4 -r 15 -c:v libx264 -b:v 1850k -pass 1 -passlogfile pl \
  -an -preset veryslow -tune animation -profile:v high -pix_fmt yuv420p -g 60 -f mp4 /dev/null
ffmpeg -y -i source.mp4 -r 15 -c:v libx264 -b:v 1850k -pass 2 -passlogfile pl \
  -an -preset veryslow -tune animation -profile:v high -pix_fmt yuv420p -g 60 \
  -movflags +faststart assets/video/matsim-demo.mp4
```

Dropping 30 fps to 15 fps is what makes it work: at 30 fps the same bitrate starves every
frame and the individual agents smear into blobs. `-tune animation` suits the flat synthetic
graphics. Keep the result comfortably under 25 MiB — raising the bitrate to fill the limit
gained no visible quality. The video carries no audio track.

`preload="none"` plus a poster image means the 21 MiB file is not fetched until someone
presses play.

## Figures

The site carries no figures at present. Only figures from **published** work belong
here; anything from unpublished work stays out.

## Content rules

- Only results that are already published. No numbers from unpublished work.
- Use MAZ (Micro Analysis Zone) for demand resolution — not "coordinate level".

## Run locally

Open `index.html` directly in a browser, or serve it:

```bash
cd site
python3 -m http.server 8000
# visit http://localhost:8000
```

## Deploy

Published with GitHub Pages from `main` at the repository root, live at
<https://seankwon469.github.io>. Pushing to `main` redeploys; a build takes
under a minute.

```bash
git add -A && git commit -m "..." && git push
```

`.nojekyll` keeps Jekyll from processing the files. `robots.txt` and a `noindex`
meta tag on every page keep the site out of search engines — remove both if you
ever want it indexed.

## To do / gaps

- [ ] Profile photo (none in source assets — currently uses a monogram placeholder).
- [ ] CV PDF (marked "to be added" on the original site).
- [ ] Paper links (DOIs / URLs) for each publication.
- [ ] Google Scholar profile URL — the profile is intentionally private, so no link is shown.
- [x] LinkedIn profile URL — recovered from the Google Sites export.
- [ ] Research Projects section — rebuild once the underlying work is published.
- [ ] Confirm whether the ranking work belongs in Research Areas (see notes).

## Credits

Content was migrated from an earlier Google Sites page. That page is not linked from
this site and its URL is deliberately not recorded here.
