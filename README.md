# Robot Lab Portfolio

An interactive developer portfolio in **four styles**, built with plain HTML, CSS and JavaScript. No build step, no framework: open a file and it runs.

**Live:** https://yousef-portfolio.loophole.site

| Style | File | Idea |
|---|---|---|
| **Robot Lab** | [`index.html`](index.html) | Drive a robot through a 3D lab (Three.js). Each zone is a field, each pillar a project. WASD / arrows / tap the floor, `E` to open. |
| **YousefOS** | [`styles/os.html`](styles/os.html) | The portfolio is a Linux desktop: draggable windows, a dock, a working terminal (`help`, `neofetch`, `open rag`…) and a point-cloud wallpaper that morphs per app. |
| **Spotlight** | [`styles/spotlight.html`](styles/spotlight.html) | Clean, recruiter-first two-column layout with a cursor spotlight, live section nav, `⌘K` command palette and light/dark themes. |
| **Desk Story** | [`styles/desk-story.html`](styles/desk-story.html) | An illustrated night-time desk pinned while you scroll; the monitor, ESP32 board and phone change with each chapter. |

Every project opens a **"How it works"** case study: summary, key numbers, the pipeline step by step, design decisions, stack and a link to the code.

## Make it yours

All content lives in one file: **[`data.js`](data.js)**. Every style reads from it.

- `EMAIL`, `LINKS` – contact and profile links (`cv` is your CV link)
- `PROJECTS` – each project: `title`, `tag`, `cat`, `big` (headline number), `summary`, `kpis`, `flow` (how-it-works steps), `notes`, `stack`, `repo`, optional `bars` (a small chart) and `extra` (a second link)
- `CATS` – project categories (`cv`, `nlp`, `ml`, `iot`, `apps`)
- `EXPERIENCE`, `STACK`

Then change the name and intro text inside the HTML file of the style you use. In `index.html`, the CV buttons are plain links near the top; point them at your own CV.

Run it locally:

```bash
python3 -m http.server 8000
# open http://localhost:8000  (and /styles/os.html, /styles/spotlight.html, /styles/desk-story.html)
```

## Deploy

**Any static host works** (GitHub Pages, Netlify, Vercel, Cloudflare Pages): upload the folder as-is.

**Self-hosted** (how the live site runs): [`deploy/portfolio.service`](deploy/portfolio.service) serves the folder on `127.0.0.1:8093` with systemd, and [`deploy/portfolio-tunnel.service`](deploy/portfolio-tunnel.service) exposes it over HTTPS with a [loophole](https://loophole.cloud) tunnel. Adjust the user, paths and hostname, then:

```bash
sudo cp deploy/*.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now portfolio.service portfolio-tunnel.service
```

## Built with

[Three.js](https://threejs.org) (r128) · [GSAP](https://gsap.com) + ScrollTrigger · [Lenis](https://lenis.darkroom.engineering) · Google Fonts, all loaded from CDNs.

The line figures on each project page are [hairline](https://github.com/lucasmarkes/hairline) by Lucas Markes (MIT), vendored in [`vendor/`](vendor).

Voice lines in [`voice/`](voice) were generated with a neural text-to-speech voice; the page falls back to the browser's own speech if a file is missing.

The four styles are original code, inspired by well-known open-source portfolios: Bruno Simon's drivable folio, Renovamen's playground-macos, Brittany Chiang's v4 and Albino Tonnina's illustrated desk.

## License

[MIT](LICENSE) – use it, fork it, make it yours. A link back is appreciated.
