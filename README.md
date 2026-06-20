# Nihang Singh Armory

## Project

Nihang Singh Armory is a curated single-page site showcasing antique blades and the martial heritage of the Nihang — the sovereign warrior order of the Khalsa.

## Setup

Clone the repository and serve locally:

```bash
git clone <repo-url>
cd nihang-singh-armory
python3 -m http.server 8080
```

Open `http://localhost:8080` in your browser.

## Formspree

1. Sign up at https://formspree.io and create a form.
2. Copy the form ID (looks like `f/XXXXXXXX`).
3. Replace `YOUR_FORMSPREE_ID` in `index.html` with your Form ID.
4. Connect Google Sheets via the Formspree dashboard integrations and select a sheet named `Nihang Singh Armory — Inquiries` with columns: `Date | Sword | Email | Phone | Message`.

## GitHub Pages + Custom Domain

Enable GitHub Pages in the repository settings and set a `CNAME` to `nihangsingh.com`.

## Adding a sword

Use the ADD_SWORD skill in Claude Code.

## Removing a sword

Use the REMOVE_SWORD skill in Claude Code.

## Replacing the hero video

Rename your video file to `hero.mp4` and drop it in the root folder.

## Video Tips

- Keep the hero video filename as `hero.mp4`.
- Place `hero.mp4` in the same folder as `index.html` (project root).
- For better compression support, optionally add a `hero.webm` source in `index.html` before the MP4 source.
- Recommended export: H.264 MP4, 1920x1080 (or 3840x2160 for 4K), target bitrate around 5-8 Mbps.
- Keep file size reasonable (about 10-20 MB or less) to improve load speed.
- Add a poster image such as `hero-poster.jpg` and reference it on the video tag with `poster="hero-poster.jpg"`.

## Replacing the logo

Update the `#logo-slot` div in `index.html` with your logo image tag.
